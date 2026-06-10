# Enunciado — Week 13: Microservicios

## Qué viene dado en `week-13-start`

El start llega con **dos proyectos** ya en el repo:

**`monolith/`** — Spring Boot funcionando con:
- `OrderService` que llama directamente a `NotificationModule` (acoplado).
- `NotificationClient` con firma definida pero implementación vacía (`// TODO`).
- Test en rojo: verifica que el monolito llama a `notification-service` vía HTTP con `MockRestServiceServer`.

**`notification-service/`** — Proyecto Spring Boot con:
- `pom.xml`, clase `main` y `application.properties` listos.
- `NotificationController` con el método definido pero retornando `null`.
- Test en rojo: `@WebMvcTest` que verifica el `POST /notifications`.

Tu trabajo es hacer los 2 tests en rojo pasar — uno en cada proyecto.

---

## Contexto del reto

**Indra Logistics** quiere que el servicio de notificaciones sea independiente: propio proceso, propio despliegue, sin acceso a la BD de pedidos.

## Lo que debes implementar

**Tarea 1 — Completar el endpoint en `notification-service`**

```java
@PostMapping("/notifications")
@ResponseStatus(HttpStatus.ACCEPTED)
public void send(@Valid @RequestBody NotificationRequest request) {
    log.info("Sending {} to {}", request.type(), request.recipient());
    // En esta sesión: solo loguear. El envío real es bonus.
}
```

`NotificationRequest` es un record con:
- `@Email String recipient`
- `@NotNull NotificationType type`
- `Map<String, Object> payload`

El test en rojo verificará: `POST /notifications` con body válido → `202 Accepted`.

**Tarea 2 — Conectar el monolito con `RestClient`**

Completa `NotificationClient` para que llame al servicio:
```java
@Component
public class NotificationClient {
    private final RestClient restClient;

    public void notify(NotificationRequest request) {
        try {
            restClient.post()
                .uri("/notifications")
                .body(request)
                .retrieve()
                .toBodilessEntity();
        } catch (Exception e) {
            log.warn("notification-service no disponible: {}", e.getMessage());
            // degradación elegante — no propagar la excepción
        }
    }
}
```

El test en rojo usa `MockRestServiceServer` para verificar que `OrderService` llama a `/notifications` cuando confirma un pedido.

## Restricciones técnicas (para todos)

- `notification-service` sin acceso a la BD del monolito.
- El monolito debe degradarse elegantemente si el servicio no responde.
- **Criterio no funcional (operación)**: el fallo del `notification-service` no debe causar un error `500` en el monolito.

## Criterio de aceptación del PR

- [ ] Test de `notification-service` en verde (202 para request válida, 400 para inválida)
- [ ] Test de `MockRestServiceServer` en el monolito en verde
- [ ] Degradación elegante implementada en `NotificationClient`
- [ ] `mvn verify` en verde en ambos proyectos

## Bonus (opcional)

- Agregar un `HealthIndicator` en el monolito que verifique disponibilidad del `notification-service`.
- Implementar retry con `Spring Retry` (`@Retryable`) en `NotificationClient`.
