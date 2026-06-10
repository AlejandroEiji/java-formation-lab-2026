# Week 15 — Azure DevOps Pipelines (CI)

**Fecha**: 2026-10-08 · **Paquete**: Micro + Cloud + DevOps

## Objetivo

Crear un pipeline CI en Azure DevOps que ejecute build, tests y quality gate en cada PR, bloqueando el merge si algún paso falla.

## Contexto técnico

**Brecha QC atacada**: Azure DevOps (60%) — la brecha más grande del QC.  
Un pipeline CI que funciona es la diferencia entre un equipo que entrega con confianza y uno que descubre bugs en producción. Esta sesión construye ese pipeline desde cero.

## Agenda de la sesión

| Tiempo | Actividad |
|--------|-----------|
| 0–10' | Demo: anatomía de `azure-pipelines.yml`, triggers y stages |
| 10–45' | Reto: pipeline CI con build + test + quality gate |
| 45–55' | Validación: pipeline verde en Azure DevOps, PR bloqueado si falla |
| 55–60' | Cierre: `week-15-solution`, optimización de tiempos con cache |
