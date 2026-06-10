# Criterios de evaluación — Week 10

## Checklist del reviewer

### Transaccionalidad
- [ ] `@Transactional` solo en la capa de servicio
- [ ] `rollbackFor = InsufficientFundsException.class` presente (checked exception)
- [ ] `TransferAuditService` usa `propagation = REQUIRES_NEW`
- [ ] Sin self-invocation transaccional

### Tests
- [ ] Test: transferencia exitosa → saldos correctos
- [ ] Test: saldo insuficiente → rollback, saldos sin cambio
- [ ] Test: log de auditoría guardado aunque transferencia falle
- [ ] `mvn verify` en verde

### Calidad
- [ ] Sin `@Transactional` en controller o repository
- [ ] La atomicidad es evidente en el código (una sola unidad de trabajo)

## Escala de madurez

| Junior | Semi-senior | Senior | Experto |
|--------|-------------|--------|---------|
| @Transactional básico, test de éxito | rollbackFor correcto, REQUIRES_NEW | Isolation justificado, @Sql en tests | Diseña la estrategia transaccional completa del dominio bancario |
