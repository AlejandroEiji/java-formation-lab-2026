# Criterios de evaluación — Week 18

## Checklist del reviewer

### Correlation ID
- [ ] `CorrelationIdFilter` implementado como `OncePerRequestFilter`
- [ ] MDC configurado con `correlationId`
- [ ] Header `X-Correlation-ID` en la respuesta
- [ ] MDC limpiado al finalizar la request
- [ ] `correlationId` visible en los logs (captura en el PR)

### Métricas
- [ ] `meterRegistry.counter("orders.processed", ...)` implementado
- [ ] `GET /actuator/metrics/orders.processed` responde (captura en el PR)
- [ ] Endpoint Prometheus expuesto (`/actuator/prometheus`)

### Application Insights
- [ ] Dependencia agregada al `pom.xml`
- [ ] Connection string leída desde el entorno (no hardcodeada)
- [ ] Sin `APPLICATIONINSIGHTS_CONNECTION_STRING` en ningún archivo del repo

### Tests
- [ ] Test unitario del `CorrelationIdFilter`
- [ ] `mvn verify` en verde

## Escala de madurez

| Junior | Semi-senior | Senior | Experto |
|--------|-------------|--------|---------|
| CorrelationIdFilter funcional, métrica básica | Application Insights configurado, test del filtro | Propagación del correlationId en llamadas salientes | Propone estrategia de observabilidad completa: logs + métricas + trazas (OpenTelemetry) |

---

## Cierre del Plan de Formación 2026

### Lo que cubrimos en 18 semanas

| Paquete | Sesiones | Brecha QC atacada |
|---------|----------|------------------|
| Arranque | 1 | Setup inicial |
| SOLID + TDD | 4 | 77% |
| Spring Web / Testing | 3 | 77–83% |
| Hibernate / JPA | 4 | 64% |
| Micro + Cloud + DevOps | 6 | 60–76% |

### Próximos pasos sugeridos para 2027

- Arquitectura Hexagonal / Clean Architecture
- Event-Driven con Kafka o Azure Service Bus
- Kubernetes (AKS)
- Java 25 LTS (virtual threads, structured concurrency)
