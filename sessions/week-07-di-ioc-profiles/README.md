# Week 07 — DI/IoC: Profiles y Wiring

**Fecha**: 2026-08-13 · **Paquete**: Spring Web / Testing

## Objetivo

Configurar el contenedor Spring correctamente para múltiples entornos: inyección por constructor obligatoria, uso de `@Profile`, `@Conditional` y separación de configuración por entorno.

## Contexto técnico

**Brecha QC atacada**: Spring avanzado / DI (77–83%)  
El error más frecuente en proyectos: configuración hardcodeada, beans que se comportan diferente en local vs producción, o `@Autowired` en campo que ocultan dependencias. Esta sesión lo corrige en raíz.

## Agenda de la sesión

| Tiempo | Actividad |
|--------|-----------|
| 0–10' | Demo: @Autowired en campo vs constructor, profiles en acción |
| 10–45' | Reto: configurar beans distintos por perfil (ver `enunciado.md`) |
| 45–55' | Validación: tests con `@ActiveProfiles`, beans correctos por entorno |
| 55–60' | Cierre: `week-07-solution`, 12-factor app aplicado |
