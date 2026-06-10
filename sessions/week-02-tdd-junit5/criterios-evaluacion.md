# Criterios de evaluación — Week 02

## Checklist del reviewer

### TDD
- [ ] Existen commits de test anteriores a commits de implementación
- [ ] Los tests fallan antes de que exista la implementación (se deduce del historial)

### Tests
- [ ] Al menos 5 tests cubriendo los escenarios del enunciado
- [ ] Tests para casos borde: monto cero, moneda desconocida, cliente inválido
- [ ] `@DisplayName` o nombres de método que explican el escenario
- [ ] Sin `if` ni lógica condicional dentro de los tests

### Funcionalidad
- [ ] Cálculo correcto para STANDARD y PREMIUM
- [ ] Recargo de EUR aplicado correctamente
- [ ] `UnsupportedCurrencyException` lanzada para monedas desconocidas
- [ ] `IllegalArgumentException` para montos <= 0
- [ ] Redondeo a 2 decimales correcto

### Calidad
- [ ] `mvn verify` en verde
- [ ] Sin código de producción sin tests que lo respalde

## Escala de madurez

| Junior | Semi-senior | Senior | Experto |
|--------|-------------|--------|---------|
| Tests post-implementación, casos básicos | Tests primero, cubre casos borde | Tests parametrizados, @Nested, diseño guiado por tests | Identifica ambigüedades en los requisitos y los convierte en tests adicionales |
