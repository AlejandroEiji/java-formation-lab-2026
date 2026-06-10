# Enunciado — Week 03: SOLID (SRP/OCP)

## Qué viene dado en `week-03-start`

El start llega con:
- `OrderProcessor` original con todo mezclado (punto de partida del análisis).
- `StockValidator` ya extraída y testeada — sirve de modelo para la siguiente extracción.
- `OrderNotifier` ya extraída y testeada.
- Tests existentes de `StockValidator` y `OrderNotifier` en verde.
- Enum `DiscountType` con valores `STANDARD` y `SEASONAL`.

Tu trabajo es completar **2 tareas concretas** sobre ese andamiaje.

---

## Contexto del reto

El equipo de **Indra Retail** tiene una clase `OrderProcessor` que sigue mezclando la lógica de descuentos junto con la orquestación. Cada vez que aparece un nuevo tipo de descuento hay que modificar la misma clase, lo que rompe tests que no tienen nada que ver con descuentos.

## Lo que debes implementar

**Tarea 1 — SRP: extraer `DiscountCalculator`**

Mueve la lógica de descuentos de `OrderProcessor` a una clase `DiscountCalculator`:
```java
public class DiscountCalculator {
    public BigDecimal apply(BigDecimal price, DiscountType type) { ... }
}
```
`OrderProcessor` debe quedar solo con coordinación — sin `if` de descuento.

**Tarea 2 — OCP: agregar tipo `LOYALTY`**

Agrega `LOYALTY` (15% de descuento para clientes con más de 12 meses) **sin modificar** el código existente de `DiscountCalculator`:
- Agrega el valor al enum `DiscountType`.
- Implementa el caso en `DiscountCalculator` como una entrada nueva, sin tocar los casos `STANDARD` y `SEASONAL`.
- Escribe 1 test para `LOYALTY`.

## Restricciones técnicas (para todos)

- Los tests del `week-03-start` deben seguir en verde.
- `OrderProcessor` no debe contener lógica de descuentos.
- La adición de `LOYALTY` no debe modificar los tests existentes de `STANDARD` y `SEASONAL`.
- **Criterio no funcional (calidad)**: `DiscountCalculator` tiene una única razón para cambiar — las reglas de descuento.

## Criterio de aceptación del PR

- [ ] `DiscountCalculator` creada y usada desde `OrderProcessor`
- [ ] `OrderProcessor` sin lógica de descuentos
- [ ] `LOYALTY` funcional sin modificar tests existentes
- [ ] 1 test nuevo para `LOYALTY`
- [ ] `mvn verify` en verde

## Bonus (opcional)

- Usar una **sealed interface** de Java 21 para modelar los tipos de descuento en lugar del enum.
- Aplicar el patrón **Strategy** para que `DiscountCalculator` sea extensible sin tocar la clase.
