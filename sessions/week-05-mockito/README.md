# Week 05 — Mockito: Buenas Prácticas

**Fecha**: 2026-07-30 · **Paquete**: SOLID + TDD

## Objetivo

Escribir tests con Mockito que sean **confiables y no frágiles**: mockear solo lo necesario, verificar comportamiento sin atarse a detalles de implementación, y evitar los anti-patrones más comunes.

## Contexto técnico

**Brecha QC atacada**: Testing (79%)  
El anti-patrón más frecuente en la comunidad: tests que mockean todo y verifican que se llamó al mock en lugar de verificar el resultado. Esta sesión ataca ese hábito directamente.

## Agenda de la sesión

| Tiempo | Actividad |
|--------|-----------|
| 0–10' | Demo: test frágil vs test robusto con Mockito |
| 10–45' | Reto: testear `PaymentService` mockeando dependencias externas |
| 45–55' | Validación: tests pasan, discusión de qué mockear y qué no |
| 55–60' | Cierre: `week-05-solution`, lista de anti-patrones |
