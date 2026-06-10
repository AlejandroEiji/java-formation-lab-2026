# Enunciado — Week 04: Patrones (Strategy/Factory)

## Qué viene dado en `week-04-start`

El start llega con:
- Interfaz `ShippingStrategy` ya definida con los 3 métodos (`calculateCost`, `estimatedDays`, `channelName`).
- `StandardShipping` ya implementada y con su test en verde — sirve de modelo exacto.
- `ShippingService` con un `if-else` de canal que debes eliminar.
- Clase `ShippingStrategyFactory` con firma definida pero sin implementación (método retorna `null`).
- Test de `ShippingService` en rojo: falla porque la factory retorna `null`.

Tu trabajo es completar **2 estrategias + la factory** para que todo quede en verde.

---

## Contexto del reto

**Indra Logistics** necesita agregar los canales `EXPRESS` y `STORE_PICKUP` al sistema de envíos. Cada vez que se agrega uno, el QA reporta regresiones en los canales anteriores porque todo está en el mismo bloque `if-else`.

## Lo que debes implementar

**Tarea 1 — 2 estrategias nuevas**

Siguiendo exactamente el modelo de `StandardShipping`:
- `ExpressShipping`: costo = `weightKg * 8.0 + distanceKm * 0.05`; 1 día; canal `EXPRESS`.
- `StorePickup`: costo = `0.0`; 0 días; canal `STORE_PICKUP`.
- 1 test por cada estrategia (copiar la estructura del test de `StandardShipping`).

**Tarea 2 — Completar `ShippingStrategyFactory`**

```java
public ShippingStrategy getStrategy(String channelCode) {
    return switch (channelCode) {
        case "STANDARD"     -> new StandardShipping();
        case "EXPRESS"      -> new ExpressShipping();
        case "STORE_PICKUP" -> new StorePickup();
        default             -> throw new UnknownChannelException(channelCode);
    };
}
```

Elimina el `if-else` de canal en `ShippingService` usando la factory.

## Restricciones técnicas (para todos)

- `ShippingService` no debe referenciar `ExpressShipping` ni `StorePickup` directamente.
- Agregar una 4.ª estrategia no debe requerir modificar `ShippingService`.
- **Criterio no funcional (calidad)**: cada estrategia en su propio archivo; los tests de `StandardShipping` no deben verse afectados.

## Criterio de aceptación del PR

- [ ] `ExpressShipping` y `StorePickup` implementadas con su test
- [ ] `ShippingStrategyFactory` completa (3 canales + excepción para desconocido)
- [ ] `ShippingService` sin `if-else` de canal
- [ ] Tests del start siguen en verde
- [ ] `mvn verify` en verde

## Bonus (opcional)

- Registrar las estrategias como `@Component` de Spring y que la factory las descubra automáticamente desde `List<ShippingStrategy>`.
- Agregar `SameDayDelivery` sin tocar ninguna clase existente.
