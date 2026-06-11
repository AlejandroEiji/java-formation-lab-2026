# Week 14 — Podman + Compose

**Fecha**: 2026-10-01 · **Paquete**: Micro + Cloud + DevOps

## Objetivo

Contenerizar la aplicación Spring Boot y orquestar el stack completo (app + base de datos) con Podman Compose para garantizar un entorno reproducible entre dev y CI.

> **¿Por qué Podman?** Por política de licencias se usa Podman en lugar de Docker Desktop. La sintaxis de Containerfile/Dockerfile y del archivo `compose.yml` es idéntica — el conocimiento aplica en ambos entornos.

## Contexto técnico

**Brecha QC atacada**: Cloud/Docker (76%), CI/CD (15% encuesta)  
"En mi máquina funciona" es el síntoma de falta de contenedores. Con Podman Compose el entorno de desarrollo es idéntico al de CI y staging.

## Agenda de la sesión

| Tiempo | Actividad |
|--------|-----------|
| 0–10' | Demo: `podman run` vs `podman compose up`, layers en Containerfile |
| 10–45' | Reto: Containerfile multi-stage + compose con app + Postgres |
| 45–55' | Validación: `podman compose up` arranca todo, health checks pasan |
| 55–60' | Cierre: `week-14-solution`, optimización de layers y tamaño de imagen |
