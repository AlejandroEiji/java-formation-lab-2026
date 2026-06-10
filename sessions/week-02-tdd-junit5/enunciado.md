# Enunciado — Week 02: TDD con JUnit 5

## Contexto del reto

El equipo de **Indra Payments** necesita una calculadora de comisiones para su plataforma de pagos internacionales. El Product Owner entregó los criterios de aceptación, pero **no existe ningún código todavía**. Tu trabajo es implementar la lógica usando TDD estricto: escribe el test primero, hazlo fallar, luego escribe el mínimo código para que pase.

## Lo que debes implementar

Usando el ciclo **red → green → refactor**:

1. `CommissionCalculator.calculate(amount, currency, clientType)` debe retornar la comisión aplicable:
   - Cliente `STANDARD`: 2.5% del monto
   - Cliente `PREMIUM`: 1.0% del monto
   - Moneda `USD`: sin recargo adicional
   - Moneda `EUR`: recargo fijo de 0.50
   - Moneda desconocida: lanzar `UnsupportedCurrencyException`
2. El monto debe ser mayor a cero; lanzar `IllegalArgumentException` si no.
3. El resultado debe redondearse a 2 decimales.

## Restricciones técnicas (para todos)

- **El test debe escribirse antes que la implementación** (commits separados recomendados: `test: ...` luego `feat: ...`).
- Usar anotaciones JUnit 5: `@Test`, `@DisplayName`, `@ParameterizedTest`, `@ValueSource` o `@CsvSource`.
- Sin lógica condicional en los tests (no `if` dentro de un test).
- **Criterio no funcional (calidad)**: los tests deben ser el primer lugar donde se entiende qué hace el sistema — deben leerse como especificaciones.

## Criterio de aceptación del PR

- [ ] Tests escritos antes del código (se aprecia en el historial de commits)
- [ ] Al menos 5 tests cubriendo los escenarios descritos
- [ ] `mvn verify` en verde
- [ ] Sin lógica condicional dentro de los métodos de test
- [ ] Nombres de test descriptivos con `@DisplayName`

## Bonus (opcional)

- Implementar `@ParameterizedTest` con `@CsvSource` para los escenarios de cliente/moneda.
- Agregar un test de integración que use `@Nested` para agrupar escenarios por tipo de cliente.
