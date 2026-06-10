# Week 14 — Docker + Compose

**Fecha**: 2026-10-01 · **Paquete**: Micro + Cloud + DevOps

## Objetivo

Dockerizar la aplicación Spring Boot y orquestar el stack completo (app + base de datos) con Docker Compose para garantizar un entorno reproducible entre dev y CI.

## Contexto técnico

**Brecha QC atacada**: Cloud/Docker (76%), CI/CD (15% encuesta)  
"En mi máquina funciona" es el síntoma de falta de Docker. Con Docker Compose el entorno de desarrollo es idéntico al de CI y staging.

## Agenda de la sesión

| Tiempo | Actividad |
|--------|-----------|
| 0–10' | Demo: `docker run` vs `docker compose up`, layers en Dockerfile |
| 10–45' | Reto: Dockerfile multi-stage + compose con app + Postgres |
| 45–55' | Validación: `docker compose up` arranca todo, health checks pasan |
| 55–60' | Cierre: `week-14-solution`, optimización de layers y tamaño de imagen |
