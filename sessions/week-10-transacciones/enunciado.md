# Enunciado — Week 10: Transacciones

## Qué viene dado en `week-10-start`

El start llega con:
- Entidades `Account` con campos `id`, `owner`, `balance`.
- `TransferService` con el método `transfer()` esquelético: descuenta y acredita, pero **sin `@Transactional`** — los tests demuestran que el saldo queda inconsistente si algo falla.
- `TransferAuditService` con el método `log()` sin implementar.
- 2 tests en rojo que describen exactamente el comportamiento esperado.

Tu trabajo es hacer esos 2 tests pasar con las anotaciones correctas.

---

## Contexto del reto

**Indra Bank** ha tenido incidentes en producción donde el débito se aplica pero el crédito falla, dejando el sistema inconsistente. Además, el log de auditoría se pierde cuando la transferencia falla porque está en la misma transacción.

## Lo que debes implementar

**Tarea 1 — Hacer `transfer()` atómico**

Anota `transfer()` correctamente:
```java
@Transactional(rollbackFor = InsufficientFundsException.class)
public void transfer(Long fromId, Long toId, BigDecimal amount) { ... }
```
`InsufficientFundsException` es una **checked exception** — sin `rollbackFor` Spring no hace rollback.

**Tarea 2 — Log de auditoría independiente**

Implementa `TransferAuditService.log()` con propagación independiente:
```java
@Transactional(propagation = Propagation.REQUIRES_NEW)
public void log(TransferEvent event) { ... }
```
Esto garantiza que el log se guarda aunque la transferencia haga rollback.

**Los 2 tests del start validan exactamente esto:**
- Test 1: saldo insuficiente → ambas cuentas sin cambio (rollback verificado).
- Test 2: transferencia fallida → log de auditoría guardado de todas formas.

## Restricciones técnicas (para todos)

- `@Transactional` solo en la capa de servicio — nunca en controller ni repository.
- Sin llamadas `@Transactional` entre métodos de la misma clase (self-invocation).
- **Criterio no funcional (operación)**: el log de auditoría debe sobrevivir al rollback de la transferencia — demostrado por el Test 2.

## Criterio de aceptación del PR

- [ ] Test 1 (rollback por saldo insuficiente) en verde
- [ ] Test 2 (log survives rollback) en verde
- [ ] `rollbackFor = InsufficientFundsException.class` presente
- [ ] `TransferAuditService` con `REQUIRES_NEW`
- [ ] `mvn verify` en verde

## Bonus (opcional)

- Agregar un 3.er test: transferencia exitosa con saldos correctos verificados.
- Explicar en el PR por qué `REQUIRES_NEW` en lugar de `NESTED` para este caso.
