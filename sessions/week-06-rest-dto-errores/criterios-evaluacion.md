# Criterios de evaluación — Week 06

## Checklist del reviewer

### DTOs
- [ ] `CreateOrderRequest` es un record con validaciones `@NotNull`, `@NotEmpty`, `@Size`
- [ ] `OrderResponse` no expone campos internos de la entidad JPA
- [ ] La entidad JPA no aparece en la firma del controller

### Controller
- [ ] `POST /api/orders` retorna `201 Created`
- [ ] `@Valid` presente en el parámetro del request body
- [ ] Sin lógica de negocio en el controller

### Manejo de errores
- [ ] `@RestControllerAdvice` presente
- [ ] `MethodArgumentNotValidException` → `400` con lista de errores
- [ ] `OrderNotFoundException` → `404`
- [ ] Sin stack trace en ninguna respuesta de error
- [ ] Formato de error consistente con `timestamp` y `status`

### Tests
- [ ] Al menos 1 test para el escenario exitoso (201)
- [ ] Al menos 1 test para validación fallida (400)
- [ ] `mvn verify` en verde

## Escala de madurez

| Junior | Semi-senior | Senior | Experto |
|--------|-------------|--------|---------|
| DTOs básicos, manejo de error parcial | Todos los handlers, formato consistente | Records Java 21, tests de todos los error paths, mensajes internacionalizados | Propone un contrato de error estándar para toda la API del proyecto |
