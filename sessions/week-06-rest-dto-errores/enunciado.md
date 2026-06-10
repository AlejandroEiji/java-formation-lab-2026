# Enunciado — Week 06: REST Limpio (DTO/errores)

## Contexto del reto

**Indra Retail** expone un endpoint para crear pedidos. Actualmente recibe la entidad JPA directamente en el controller, retorna la entidad completa (incluyendo datos internos) y cuando algo falla devuelve un `500` genérico con el stack trace. Los clientes del API se quejan de que no saben qué campos son inválidos.

## Lo que debes implementar

1. Crea `CreateOrderRequest` (record Java 21) con:
   - `customerId` — no nulo, no vacío
   - `items` — lista no vacía, mínimo 1 elemento
   - `deliveryAddress` — no nulo, mínimo 10 caracteres
2. Crea `OrderResponse` (record) con solo los campos públicos: `orderId`, `status`, `totalAmount`, `estimatedDelivery`.
3. Crea `POST /api/orders` en `OrderController` que:
   - Recibe `@Valid @RequestBody CreateOrderRequest`
   - Retorna `201 Created` con `OrderResponse`
4. Crea `@RestControllerAdvice` con handlers para:
   - `MethodArgumentNotValidException` → `400` con lista de errores de campo
   - `OrderNotFoundException` → `404` con mensaje descriptivo
   - Cualquier otra excepción → `500` con mensaje genérico (sin stack trace)
5. El formato de error debe ser consistente:
   ```json
   { "timestamp": "...", "status": 400, "errors": ["campo: mensaje"] }
   ```

## Restricciones técnicas (para todos)

- Sin lógica de negocio en el controller — solo delegación al service.
- La entidad JPA no debe salir del controller ni como parámetro ni como retorno.
- **Criterio no funcional (operación)**: el cliente del API nunca debe recibir un stack trace — solo mensajes de error legibles.

## Criterio de aceptación del PR

- [ ] `CreateOrderRequest` con validaciones Bean Validation
- [ ] `OrderResponse` separado de la entidad
- [ ] `POST /api/orders` retorna `201` con el body correcto
- [ ] `@RestControllerAdvice` maneja los 3 escenarios de error
- [ ] `mvn verify` en verde

## Bonus (opcional)

- Agregar `@Validated` a nivel de controller para validar parámetros de query/path.
- Internacionalizar los mensajes de error con `messages.properties`.
