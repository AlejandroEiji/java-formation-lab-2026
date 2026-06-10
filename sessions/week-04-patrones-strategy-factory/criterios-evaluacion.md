# Criterios de evaluación — Week 04

## Checklist del reviewer

### Strategy
- [ ] Interfaz `ShippingStrategy` con los 3 métodos requeridos
- [ ] 3 implementaciones concretas, cada una en su propio archivo
- [ ] `ShippingService` no referencia ninguna clase concreta de estrategia

### Factory
- [ ] `ShippingStrategyFactory.getStrategy()` funciona para los 3 canales
- [ ] `UnknownChannelException` lanzada para canal desconocido
- [ ] Agregar una nueva estrategia no requiere modificar `ShippingService`

### Tests
- [ ] Al menos 1 test por estrategia (independiente)
- [ ] Test para canal desconocido en la Factory
- [ ] `mvn verify` en verde

### Calidad
- [ ] Sin `if-else` de canal en `ShippingService`
- [ ] Sin duplicación de lógica entre estrategias

## Escala de madurez

| Junior | Semi-senior | Senior | Experto |
|--------|-------------|--------|---------|
| Strategy funcional, Factory con if-else | Factory limpia, tests por estrategia | Auto-descubrimiento con Spring @Component, OCP garantizado | Propone extensiones: decoradores, estrategias compuestas |
