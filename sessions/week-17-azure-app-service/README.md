# Week 17 — Azure App Service

**Fecha**: 2026-10-22 · **Paquete**: Micro + Cloud + DevOps

## Objetivo

Desplegar la aplicación en Azure App Service con configuración segura: Application Settings (sin secretos en código), deployment slots para zero-downtime, y troubleshooting con logs en la nube.

## Contexto técnico

**Brecha QC atacada**: Cloud Azure (76%)  
App Service es el servicio más accesible para desplegar aplicaciones Java en Azure. Esta sesión cubre los tres problemas más frecuentes: secretos expuestos, downtime en deploy y "no sé qué está pasando en producción".

## Agenda de la sesión

| Tiempo | Actividad |
|--------|-----------|
| 0–10' | Demo: App Service plan, deployment slots, Application Settings vs código |
| 10–45' | Reto: deploy seguro con slot de staging y swap a producción |
| 45–55' | Validación: app viva en Azure, logs accesibles, secretos no visibles en el repo |
| 55–60' | Cierre: `week-17-solution`, costos y buenas prácticas |
