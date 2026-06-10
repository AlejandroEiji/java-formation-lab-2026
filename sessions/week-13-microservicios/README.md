# Week 13 — Microservicios: Límites y Contratos

**Fecha**: 2026-09-24 · **Paquete**: Micro + Cloud + DevOps

## Objetivo

Definir bounded contexts claros, extraer un módulo como microservicio independiente y establecer contratos REST entre servicios.

## Contexto técnico

**Brecha QC atacada**: Microservicios (86%) — la comunidad lo quiere fortalecer (23% encuesta).  
El error más frecuente: microservicios que son monolitos distribuidos — misma base de datos, mismo dominio, pero en procesos separados. Esta sesión ataca los límites correctos.

## Agenda de la sesión

| Tiempo | Actividad |
|--------|-----------|
| 0–10' | Demo: monolito distribuido vs microservicio real, bounded context |
| 10–45' | Reto: extraer el módulo de notificaciones como microservicio |
| 45–55' | Validación: servicio arranca independiente, contrato REST documentado |
| 55–60' | Cierre: `week-13-solution`, cuándo NO microservicios |
