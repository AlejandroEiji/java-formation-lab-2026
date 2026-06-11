# java-formation-lab-2026

![Java 21](https://img.shields.io/badge/Java-21-007396?logo=java)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-6DB33F?logo=springboot)
![Azure DevOps](https://img.shields.io/badge/Azure%20DevOps-CI%2FCD-0078D7?logo=azuredevops)
![Sesiones](https://img.shields.io/badge/Sesiones-18-blueviolet)

Repositorio oficial del **Plan de Formación Java 2026** — Indra Colombia (~200 personas).  
Basado en los resultados del QC 2026 COL y CA&C. Una sesión semanal, cada jueves, 1 hora.

---

## ¿Por qué este modelo?

**Un único reto intermedio para todos los seniorities.**  
El nivel se evidencia en _cómo_ resolviste el problema — no en _qué_ problema resolviste.

- Sesiones **autocontenidas**: quien no asistió puede resolver el reto con `week-XX-start` + solución publicada.
- Cada reto incluye: **1 cambio funcional + 1 prueba + 1 criterio no funcional** (calidad / performance / operación / seguridad).
- Rama `week-XX-start` disponible antes del jueves; `week-XX-solution` publicada al cierre de sesión.

### Formato de sesión (1 hora)

| Segmento | Tiempo | Contenido |
|----------|--------|-----------|
| Contexto + demo | 0–10' | Qué vamos a mejorar y por qué |
| Reto intermedio único | 10–45' | Implementación real en el repo |
| Validación | 45–55' | Tests + pipeline verde |
| Cierre | 55–60' | Solución de referencia publicada |

---

## Calendario 2026 (jueves, jul–oct)

| # | Fecha | Paquete | Sesión | Estado |
|---|-------|---------|--------|--------|
| 01 | 2026-07-02 | Arranque | Kickoff + setup Java 21 | ⏳ |
| 02 | 2026-07-09 | SOLID + TDD | TDD con JUnit 5 | ⏳ |
| 03 | 2026-07-16 | SOLID + TDD | SOLID (SRP/OCP) | ⏳ |
| 04 | 2026-07-23 | SOLID + TDD | Patrones (Strategy/Factory) | ⏳ |
| 05 | 2026-07-30 | SOLID + TDD | Mockito (buenas prácticas) | ⏳ |
| 06 | 2026-08-06 | Spring Web / Testing | REST limpio (DTO/errores) | ⏳ |
| 07 | 2026-08-13 | Spring Web / Testing | DI/IoC (profiles/wiring) | ⏳ |
| 08 | 2026-08-20 | Spring Web / Testing | WebMvcTest (slice tests) | ⏳ |
| 09 | 2026-08-27 | Hibernate / JPA | Mapeos JPA | ⏳ |
| 10 | 2026-09-03 | Hibernate / JPA | Transacciones | ⏳ |
| 11 | 2026-09-10 | Hibernate / JPA | Performance ORM | ⏳ |
| 12 | 2026-09-17 | Hibernate / JPA | JPQL + paginación + locking | ⏳ |
| 13 | 2026-09-24 | Micro + Cloud + DevOps | Microservicios | ⏳ |
| 14 | 2026-10-01 | Micro + Cloud + DevOps | Podman + compose | ⏳ |
| 15 | 2026-10-08 | Micro + Cloud + DevOps | Azure DevOps Pipelines (CI) | ⏳ |
| 16 | 2026-10-15 | Micro + Cloud + DevOps | Azure DevOps Release | ⏳ |
| 17 | 2026-10-22 | Micro + Cloud + DevOps | Azure App Service | ⏳ |
| 18 | 2026-10-29 | Micro + Cloud + DevOps | Observabilidad + cierre | ⏳ |

**Vista por mes**

| Mes | Semanas | Paquete |
|-----|---------|--------|
| Julio | 4 sesiones (sem 1–4) | Arranque + SOLID + TDD |
| Agosto | 5 sesiones (sem 5–9) | SOLID+TDD (cierre) + Spring Web + Hibernate (inicio) |
| Septiembre | 5 sesiones (sem 10–14) | Hibernate (cierre) + Micro/Cloud/DevOps (inicio) |
| Octubre | 4 sesiones (sem 15–18) | Micro/Cloud/DevOps (cierre) |

<details>
<summary>Sesiones descartadas del plan (fortalezas o bajo impacto QC)</summary>

- Git + PR hygiene → Git es fortaleza
- Maven multi-módulo → Maven es fortaleza
- DataJpaTest → cubierto dentro del paquete Hibernate
- Spring Security → no aparece en las brechas QC prioritarias
- OpenAPI → se cubre dentro de Microservicios
- Projections/read models → menor prioridad en Hibernate/JPA
</details>

---

## ¿Cómo empiezo?

1. **Lee** [REGLAS_DE_JUEGO.md](REGLAS_DE_JUEGO.md) y [docs/onboarding-java21.md](docs/onboarding-java21.md).
2. **Crea tu rama** a partir de `week-XX-start`:  
   ```bash
   git checkout week-01-start
   git checkout -b week-01/tu-alias
   ```
3. **Resuelve el reto**, haz push y abre un PR siguiendo el template.

---

## Estructura del repositorio

```
java-formation-lab-2026/
├── README.md
├── REGLAS_DE_JUEGO.md
├── .github/
│   ├── PULL_REQUEST_TEMPLATE.md
│   ├── ISSUE_TEMPLATE/badge-completado.md
│   └── labels.yml
├── docs/
│   └── onboarding-java21.md
└── sessions/
    └── week-XX-<tema>/
        ├── README.md
        ├── enunciado.md
        ├── criterios-evaluacion.md
        └── solucion-referencia/
```

---

## Stack

`Java 21` · `Spring Boot 3.x` · `Hibernate 6` · `JUnit 5` · `Mockito` · `Azure DevOps` · `Podman` · `Azure App Service`
