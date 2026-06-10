# Week 16 — Azure DevOps Release

**Fecha**: 2026-10-15 · **Paquete**: Micro + Cloud + DevOps

## Objetivo

Configurar un pipeline de release con múltiples stages (dev → prod) con aprobación manual antes de producción, variables por entorno y rollback claro.

## Contexto técnico

**Brecha QC atacada**: Azure DevOps (60%)  
El CI construye confianza en el código. El CD entrega ese código a los usuarios. Sin un release pipeline controlado, cada deploy es un evento de alto riesgo. Esta sesión lo convierte en una operación rutinaria.

## Agenda de la sesión

| Tiempo | Actividad |
|--------|-----------|
| 0–10' | Demo: release pipeline en Azure DevOps, environments y approvals |
| 10–45' | Reto: pipeline release dev → prod con aprobación (ver `enunciado.md`) |
| 45–55' | Validación: deploy a dev automático, prod requiere aprobación |
| 55–60' | Cierre: `week-16-solution`, estrategias de rollback |
