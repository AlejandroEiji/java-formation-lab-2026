# Enunciado — Week 12: JPQL + Paginación + Locking

## Qué viene dado en `week-12-start`

El start llega con:
- `ProductRepository` con una query JPQL funcional pero **sin paginación** — carga todos los registros.
- Entidad `Product` con `@Version private Long version` ya declarado.
- `InventoryService.reserveStock()` implementado pero **sin manejo de `OptimisticLockException`** — el test de concurrencia falla.
- 2 tests en rojo: uno de paginación y uno de concurrencia.

Tu trabajo es hacer esos 2 tests pasar con cambios mínimos y quirúrgicos.

---

## Contexto del reto

**Indra Retail** tiene dos bugs: el endpoint de búsqueda carga 50.000 productos en memoria y cuando dos usuarios compran el último ítem simultáneamente ambas compras se aprueban.

## Lo que debes implementar

**Tarea 1 — Agregar `Pageable` a la query existente**

La query del start es:
```java
@Query("SELECT p FROM Product p WHERE " +
       "(:name IS NULL OR LOWER(p.name) LIKE LOWER(CONCAT('%', :name, '%')))")
List<Product> searchProducts(@Param("name") String name);
```

Cámbiala para retornar `Page<Product>` y recibir `Pageable`:
```java
Page<Product> searchProducts(@Param("name") String name, Pageable pageable);
```

El test en rojo verifica: 50 productos en BD, búsqueda con `PageRequest.of(0, 10)` → `content.size() == 10` y `totalElements == 50`.

**Tarea 2 — Manejar `OptimisticLockException` en `reserveStock()`**

`reserveStock()` ya descuenta el stock. Solo falta envolver la llamada a `save()` para traducir la excepción:
```java
try {
    productRepository.save(product);
} catch (OptimisticLockException | ObjectOptimisticLockingFailureException e) {
    throw new ConcurrentModificationException("Stock modificado concurrentemente, reintenta");
}
```

El test en rojo simula 2 threads comprando el último ítem: verifica que exactamente 1 lanza `ConcurrentModificationException`.

## Restricciones técnicas (para todos)

- La paginación debe ocurrir en la query SQL — no filtrar en Java.
- Sin cambiar `FetchType.EAGER` como solución al test de concurrencia.
- **Criterio no funcional (performance)**: la query paginada no debe cargar más registros que `page.size`.

## Criterio de aceptación del PR

- [ ] Test de paginación en verde (`content.size == 10`, `totalElements == 50`)
- [ ] Test de concurrencia en verde (1 de 2 threads lanza `ConcurrentModificationException`)
- [ ] Sin `FetchType.EAGER` añadido
- [ ] `mvn verify` en verde

## Bonus (opcional)

- Agregar los filtros opcionales `minPrice` y `maxPrice` a la query paginada.
- Reemplazar la query JPQL por `Specification<Product>` con `JpaSpecificationExecutor`.
