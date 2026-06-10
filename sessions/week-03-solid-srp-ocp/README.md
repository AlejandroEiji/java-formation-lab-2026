# Week 03 — SOLID: SRP y OCP

**Fecha**: 2026-07-16 · **Paquete**: SOLID + TDD

## Objetivo

Identificar violaciones de **Single Responsibility Principle** y **Open/Closed Principle** en código real y refactorizarlas manteniendo los tests en verde.

## Contexto técnico

**Brecha QC atacada**: SOLID + TDD (77%)  
El código inicial tiene una clase que hace demasiado (viola SRP) y requiere modificación para agregar nuevos comportamientos (viola OCP). Refactorizar sin romper los tests existentes es la habilidad clave.

## Agenda de la sesión

| Tiempo | Actividad |
|--------|-----------|
| 0–10' | Demo: identificar SRP/OCP violations en código real |
| 10–45' | Reto: refactorizar `OrderProcessor` (ver `enunciado.md`) |
| 45–55' | Validación: tests en verde antes y después del refactor |
| 55–60' | Cierre: `week-03-solution`, discusión de trade-offs |
