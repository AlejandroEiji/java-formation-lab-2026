# Week 12 — JPQL: Paginación y Locking

**Fecha**: 2026-09-17 · **Paquete**: Hibernate / JPA

## Objetivo

Escribir queries JPQL robustas con `Pageable`, filtros dinámicos y control de concurrencia con `@Lock` (optimistic/pessimistic) para evitar condiciones de carrera en inventario.

## Contexto técnico

**Brecha QC atacada**: Hibernate/ORM (64%)  
Paginación incorrecta y ausencia de locking son las dos causas principales de bugs en sistemas con carga concurrente. Esta sesión cubre ambas con escenarios reales.

## Agenda de la sesión

| Tiempo | Actividad |
|--------|-----------|
| 0–10' | Demo: query sin paginación que carga 50k registros, y race condition en inventario |
| 10–45' | Reto: búsqueda paginada de productos con locking en reserva de stock |
| 45–55' | Validación: tests con paginación verificada y test de concurrencia básico |
| 55–60' | Cierre: `week-12-solution`, optimistic vs pessimistic locking |
