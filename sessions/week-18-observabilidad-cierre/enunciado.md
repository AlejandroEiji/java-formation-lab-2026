# Enunciado — Week 18: Observabilidad + Cierre

## Contexto del reto

**Indra Retail** tiene la aplicación desplegada en Azure App Service, el pipeline CI/CD funcionando, pero cuando un cliente reporta un error, el equipo tarda 2 horas en encontrar qué pasó porque los logs no tienen contexto y no hay forma de trazar una request de principio a fin.

## Lo que debes implementar

### 1. Correlation ID

Implementa un filtro de Servlet que:
- Extrae el header `X-Correlation-ID` de la request entrante (o genera uno con `UUID.randomUUID()` si no viene).
- Lo coloca en el MDC de SLF4J: `MDC.put("correlationId", correlationId)`.
- Lo propaga en la respuesta como header `X-Correlation-ID`.
- Lo limpia del MDC al finalizar la request.

```java
@Component
@Order(1)
public class CorrelationIdFilter extends OncePerRequestFilter {
    // implementar aquí
}
```

Configura `logback-spring.xml` para incluir el `correlationId` en todos los logs:
```xml
<pattern>%d{ISO8601} [%thread] [%X{correlationId}] %-5level %logger{36} - %msg%n</pattern>
```

### 2. Métricas con Micrometer

Agrega una métrica personalizada en `OrderService`:
```java
@Autowired
private MeterRegistry meterRegistry;

// En el método processOrder():
meterRegistry.counter("orders.processed", "status", result.getStatus().name()).increment();
```

Expone el endpoint de métricas:
```properties
management.endpoints.web.exposure.include=health,info,metrics,prometheus
management.endpoint.health.show-details=always
```

### 3. Conectar Application Insights (Azure)

Agrega la dependencia en `pom.xml`:
```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-spring-boot-starter</artifactId>
    <version>3.x.x</version>
</dependency>
```

Configura la connection string desde Application Settings en Azure (no hardcodeada):
```properties
applicationinsights.connection-string=${APPLICATIONINSIGHTS_CONNECTION_STRING}
```

### 4. Verificación

Documenta en el PR:
- Log con `correlationId` visible en la consola.
- Screenshot de `GET /actuator/metrics/orders.processed` con el contador.
- Screenshot de Application Insights mostrando requests trazadas (si tienes acceso a Azure).

## Restricciones técnicas (para todos)

- El `correlationId` debe aparecer en **todos** los logs de una request.
- La connection string de Application Insights no debe estar en ningún archivo del repo.
- **Criterio no funcional (operación)**: dado el `correlationId` de un error reportado por un cliente, debe ser posible encontrar todos los logs relacionados en <30 segundos.

## Criterio de aceptación del PR

- [ ] `CorrelationIdFilter` implementado y testeado
- [ ] `correlationId` en todos los logs (verificar en la consola)
- [ ] Métrica `orders.processed` expuesta en `/actuator/metrics`
- [ ] `APPLICATIONINSIGHTS_CONNECTION_STRING` leída desde el entorno
- [ ] Test unitario del `CorrelationIdFilter`
- [ ] `mvn verify` en verde

## Bonus (opcional)

- Propagar el `correlationId` en las llamadas HTTP salientes (RestClient interceptor).
- Configurar alertas en Application Insights para cuando `orders.processed{status=FAILED}` supere un umbral.

---

## Retrospectiva del plan 2026

Al cerrar esta sesión, reflexiona:

1. **¿Qué aprendiste que más te impactó?**
2. **¿Qué cambiarías en tu forma de trabajar a partir de hoy?**
3. **¿Qué tema necesita más profundidad en el plan 2027?**

Comparte tu retrospectiva en el PR de esta semana.
