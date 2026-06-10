# Criterios de evaluación — Week 03

## Checklist del reviewer

### SRP
- [ ] `OrderProcessor` solo delega, no contiene lógica de negocio
- [ ] Cada clase nueva tiene una única razón para cambiar (verificar con el reviewer)
- [ ] Al menos 3 responsabilidades separadas en clases distintas

### OCP
- [ ] El descuento `LOYALTY` se agregó sin modificar código existente de descuentos
- [ ] Es posible agregar un nuevo tipo de descuento sin tocar clases ya existentes

### Tests
- [ ] Tests existentes del start siguen pasando
- [ ] Al menos 1 test por cada clase nueva
- [ ] `mvn verify` en verde

### Calidad
- [ ] Sin duplicación de lógica entre las nuevas clases
- [ ] Inyección por constructor en todas las dependencias

## Escala de madurez

| Junior | Semi-senior | Senior | Experto |
|--------|-------------|--------|---------|
| Separa clases pero con algo de lógica en el orquestador | SRP aplicado, OCP básico con extensión | Diseño limpio, sealed classes, tests por comportamiento | Propone una arquitectura que hace imposible violar OCP para futuros descuentos |
