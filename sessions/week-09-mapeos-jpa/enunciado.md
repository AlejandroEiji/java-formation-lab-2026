# Enunciado — Week 09: Mapeos JPA

## Contexto del reto

**Indra Retail** necesita persistir el dominio de su e-commerce: un `Customer` puede tener múltiples `Order`, cada `Order` contiene múltiples `OrderItem`, y cada `OrderItem` referencia un `Product`. El modelo actual tiene todas las relaciones como `EAGER` y `cascade = ALL` en todas partes, lo que causa que borrar un producto elimine pedidos enteros.

## Lo que debes implementar

1. Entidad `Customer` con campos `id`, `name`, `email` (único), `createdAt`.
2. Entidad `Order` con `id`, `status` (enum: `PENDING`, `CONFIRMED`, `SHIPPED`), `createdAt`, relación `@ManyToOne` con `Customer`.
3. Entidad `OrderItem` con `id`, `quantity`, `unitPrice`, relación `@ManyToOne` con `Order` y `@ManyToOne` con `Product`.
4. Entidad `Product` con `id`, `name`, `price`, `stock`.
5. Reglas de mapeo:
   - `Order` → `Customer`: LAZY, sin cascade (un pedido no gestiona al cliente).
   - `Order` → `OrderItem`: LAZY, `cascade = {PERSIST, MERGE}`, `orphanRemoval = true`.
   - `OrderItem` → `Product`: LAZY, sin cascade.
6. Escribe un test de repositorio que cargue una orden con sus ítems sin `LazyInitializationException`.

## Restricciones técnicas (para todos)

- **Sin `FetchType.EAGER`** en ninguna relación — justificar en el PR si alguna excepción.
- `cascade = ALL` prohibido excepto donde se justifique explícitamente.
- Usar `@Column(nullable = false)` en todos los campos obligatorios.
- **Criterio no funcional (calidad)**: el modelo debe hacer imposible guardar un `OrderItem` huérfano (sin `Order`).

## Criterio de aceptación del PR

- [ ] 4 entidades mapeadas con las relaciones correctas
- [ ] Sin `FetchType.EAGER` ni `cascade = ALL` injustificados
- [ ] `orphanRemoval = true` en la relación Order → OrderItem
- [ ] Test que carga Order con ítems sin LazyInitializationException
- [ ] `mvn verify` en verde

## Bonus (opcional)

- Agregar `@Version` para optimistic locking en `Product`.
- Usar un `@Embeddable` para modelar `Address` dentro de `Customer`.
