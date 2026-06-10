# Criterios de evaluación — Week 13

## Checklist del reviewer

### Separación de contextos
- [ ] `notification-service` no tiene dependencia de clases del monolito
- [ ] `notification-service` no accede a la base de datos de pedidos
- [ ] El contrato del API está documentado en el README del servicio

### Endpoint
- [ ] `POST /notifications` retorna `202 Accepted`
- [ ] Validación de `recipient` como email válido
- [ ] Validación de `type` contra enum `NotificationType`

### Cliente HTTP en el monolito
- [ ] `RestClient` usado (no `RestTemplate`)
- [ ] Degradación elegante si el servicio no responde
- [ ] Test con `MockRestServiceServer`

### Tests
- [ ] `@WebMvcTest` en `notification-service`
- [ ] `mvn verify` verde en ambos proyectos

## Escala de madurez

| Junior | Semi-senior | Senior | Experto |
|--------|-------------|--------|---------|
| Servicio extrae funcionalidad, arranca independiente | MockRestServiceServer, degradación elegante | HealthIndicator, Spring Retry | Propone estrategia completa de descomposición del monolito con prioridades |
