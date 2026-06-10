# Calendario de Formación Java 2026

**Comunidad Java — Indra Colombia**  
Jueves · 1 hora · Julio – Octubre 2026

---

## Vista por paquete

### Paquete: Arranque

| # | Fecha | Sesión | Objetivo |
|---|-------|--------|----------|
| 01 | 2026-07-02 | Kickoff + setup Java 21 | Ejecutar repo + week-start/solution |

### Paquete: SOLID + TDD

| # | Fecha | Sesión | Objetivo |
|---|-------|--------|----------|
| 02 | 2026-07-09 | TDD con JUnit 5 | Requerimiento → tests |
| 03 | 2026-07-16 | SOLID (SRP/OCP) | Refactor con mantenibilidad |
| 04 | 2026-07-23 | Patrones (Strategy/Factory) | Desacoplar y testear mejor |
| 05 | 2026-07-30 | Mockito (buenas prácticas) | Tests confiables (sin fragilidad) |

### Paquete: Spring Web / Testing

| # | Fecha | Sesión | Objetivo |
|---|-------|--------|----------|
| 06 | 2026-08-06 | REST limpio (DTO/errores) | API consistente y validada |
| 07 | 2026-08-13 | DI/IoC (profiles/wiring) | Configuración correcta por entorno |
| 08 | 2026-08-20 | WebMvcTest (slice tests) | Pruebas rápidas de controllers |

### Paquete: Hibernate / JPA

| # | Fecha | Sesión | Objetivo |
|---|-------|--------|----------|
| 09 | 2026-08-27 | Mapeos JPA | Modelo persistente correcto |
| 10 | 2026-09-03 | Transacciones | Evitar fallos "local vs prod" |
| 11 | 2026-09-10 | Performance ORM | Eliminar N+1 / optimizar |
| 12 | 2026-09-17 | JPQL + paginación + locking | Consultas robustas y escalables |

### Paquete: Micro + Cloud + DevOps

| # | Fecha | Sesión | Objetivo |
|---|-------|--------|----------|
| 13 | 2026-09-24 | Microservicios | Límites + contratos claros |
| 14 | 2026-10-01 | Docker + compose | Entorno reproducible dev/CI |
| 15 | 2026-10-08 | Azure DevOps Pipelines (CI) | Build + tests + quality gate |
| 16 | 2026-10-15 | Azure DevOps Release | Entrega controlada por entorno |
| 17 | 2026-10-22 | Azure App Service | Deploy + config + troubleshooting |
| 18 | 2026-10-29 | Observabilidad + cierre | Logs + correlation + release |

---

## Vista por mes

| Mes | Semanas | Paquete |
|-----|---------|---------|
| Julio | 4 sesiones (sem 1–4) | Arranque + SOLID + TDD |
| Agosto | 5 sesiones (sem 5–9) | SOLID+TDD (cierre) + Spring Web + Hibernate (inicio) |
| Septiembre | 5 sesiones (sem 10–14) | Hibernate (cierre) + Micro/Cloud/DevOps (inicio) |
| Octubre | 4 sesiones (sem 15–18) | Micro/Cloud/DevOps (cierre) |

---

## Sesiones eliminadas (fortalezas o bajo impacto QC)

Las siguientes sesiones fueron descartadas del plan original por ser fortalezas QC o tener menor impacto en las brechas identificadas:

- Git + PR hygiene → Git es fortaleza (bien dominado por la comunidad)
- Maven multi-módulo → Maven es fortaleza
- DataJpaTest (repos) → cubierto dentro del paquete Hibernate
- Spring Security + tests → no aparece en las brechas QC prioritarias
- OpenAPI + estándares REST → se cubre dentro de Microservicios
- Projections / read models → menor prioridad dentro del paquete Hibernate/JPA
