# Week 11 — Performance ORM: Eliminar N+1

**Fecha**: 2026-09-10 · **Paquete**: Hibernate / JPA

## Objetivo

Detectar y corregir el problema N+1 usando `JOIN FETCH`, `@EntityGraph` y batch size. Medir el impacto antes y después.

## Contexto técnico

**Brecha QC atacada**: Hibernate/ORM (64%)  
El N+1 es el problema de performance más frecuente en aplicaciones con ORM. Es fácil de introducir y difícil de detectar sin las herramientas correctas. Esta sesión enseña a detectarlo y eliminarlo de forma sistemática.

## Agenda de la sesión

| Tiempo | Actividad |
|--------|-----------|
| 0–10' | Demo: habilitar log de SQL, ver N+1 en acción con conteo de queries |
| 10–45' | Reto: detectar y corregir N+1 en listado de órdenes (ver `enunciado.md`) |
| 45–55' | Validación: conteo de queries antes vs después |
| 55–60' | Cierre: `week-11-solution`, cuándo usar JOIN FETCH vs @EntityGraph vs batch |
