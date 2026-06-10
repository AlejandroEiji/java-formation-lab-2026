# Week 09 — Mapeos JPA

**Fecha**: 2026-08-27 · **Paquete**: Hibernate / JPA

## Objetivo

Modelar relaciones entre entidades con JPA correctamente: fetch types, cardinalidades, `@JoinColumn`, y evitar los errores de mapeo más comunes que aparecen en producción.

## Contexto técnico

**Brecha QC atacada**: Hibernate/ORM (64%) — la brecha más grande del QC.  
El 80% de los bugs de producción relacionados con ORM vienen de mapeos incorrectos: EAGER donde debería ser LAZY, relaciones sin `cascade` correcto, o `@ManyToMany` sin tabla intermedia explícita.

## Agenda de la sesión

| Tiempo | Actividad |
|--------|-----------|
| 0–10' | Demo: EAGER vs LAZY, mapeos que explotan en producción |
| 10–45' | Reto: modelar Pedido/Producto/Cliente con relaciones correctas |
| 45–55' | Validación: consultas sin LazyInitializationException |
| 55–60' | Cierre: `week-09-solution`, reglas de oro de mapeo JPA |
