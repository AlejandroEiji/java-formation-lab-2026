# Week 10 — Transacciones

**Fecha**: 2026-09-03 · **Paquete**: Hibernate / JPA

## Objetivo

Entender y aplicar correctamente `@Transactional`: propagación, rollback rules, aislamiento, y la trampa del proxy de Spring que hace que las transacciones fallen silenciosamente en producción.

## Contexto técnico

**Brecha QC atacada**: Hibernate/ORM (64%)  
"Funciona en local, falla en producción" es el síntoma clásico de transacciones mal configuradas. Esta sesión cubre los 3 escenarios que más frecuentemente causan ese problema.

## Agenda de la sesión

| Tiempo | Actividad |
|--------|-----------|
| 0–10' | Demo: @Transactional self-invocation, rollback solo en RuntimeException |
| 10–45' | Reto: transferencia bancaria con transacciones correctas |
| 45–55' | Validación: tests con rollback verificado |
| 55–60' | Cierre: `week-10-solution`, checklist de transacciones |
