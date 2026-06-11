# Reglas de juego — java-formation-lab-2026

## Modelo de participación

Este repositorio sigue el modelo de **sesiones autocontenidas**: cada semana es independiente, diseñada para que quien no asistió pueda completarla con el material publicado.

> **Cada participante trabaja desde su propio fork.** No se requieren permisos en el repo central.

---

## Configuración inicial (una sola vez)

```bash
# 1. Hacer fork desde https://github.com/robinson8406/java-formation-lab-2026
#    (botón Fork en GitHub)

# 2. Clonar tu fork
git clone https://github.com/tu-alias/java-formation-lab-2026.git
cd java-formation-lab-2026

# 3. Agregar el repo central como upstream
git remote add upstream https://github.com/robinson8406/java-formation-lab-2026.git
```

---

## Ramas y flujo de trabajo

| Rama | Propósito | Quién la crea |
|------|-----------|---------------|
| `main` | Estado estable del repo | Formadores |
| `week-XX-start` | Código inicial de cada sesión | Formadores (antes del jueves) |
| `week-XX-solution` | Solución de referencia | Formadores (al cierre, min 55') |
| `week-XX/<tu-alias>` | Tu entrega personal | Participante |

### Flujo para participar en una sesión

```bash
# 1. Actualiza tu repo local
git fetch origin

# 2. Crea tu rama personal desde el start
git checkout week-XX-start
git checkout -b week-XX/tu-alias

# 3. Resuelve el reto
# ... implementa, escribe tests, verifica que el pipeline compile ...

# 4. Haz push y abre un PR hacia week-XX-start
git push origin week-XX/tu-alias
```

Abre el PR y asigna a **1 compañero** como reviewer.

---

## PR y peer review

- Usa el template en `.github/PULL_REQUEST_TEMPLATE.md`.
- El reviewer debe validar el checklist de `criterios-evaluacion.md` de la sesión.
- **Sin PR aprobado = sesión pendiente** (no bloquea asistencia ni acceso a la siguiente sesión; sí bloquea el badge).

---

## Badges

Al completar una sesión con PR aprobado, abre un issue con:
- **Título**: `✅ [week-XX] tu-alias completó la sesión`
- **Label**: `completado`
- El formador responsable cerrará el issue como evidencia.

---

## Convenciones de commit

Seguimos [Conventional Commits](https://www.conventionalcommits.org/):

```
feat:     nueva funcionalidad
fix:      corrección de bug
test:     añadir o modificar tests
refactor: refactorización sin cambio de comportamiento
docs:     documentación
chore:    tareas de mantenimiento (deps, config)
session:  cambios propios de una sesión de formación
```

---

## Convenciones de código

- Inyección **siempre por constructor** (nunca `@Autowired` en campo).
- Sin lógica de negocio en controladores — solo delegación.
- Mínimo **1 test por clase nueva** introducida en el reto.
- Nombres en inglés para código; español para docs y comentarios del reto.

---

## Preguntas frecuentes

**¿Puedo resolver sesiones pasadas?** Sí, `git fetch upstream` y creá tu rama desde el `week-XX-start` correspondiente.  
**¿Puedo mirar la solución antes de intentarlo?** Está publicada, pero te privás del aprendizaje 🙂  
**¿Qué stack necesito tener instalado?** Ver [docs/onboarding-java21.md](docs/onboarding-java21.md).  
**¿Necesito permisos en el repo central?** No. Solo necesitás tu cuenta GitHub gratuita y hacer fork.

---

## Para formadores

### Estructura de cada sesión

Cada sesión dura **1 hora** y sigue este formato fijo:

| Segmento | Tiempo | Contenido |
|----------|--------|-----------|
| Contexto + demo | 0–10' | Qué vamos a mejorar, por qué importa, demo rápida del código inicial |
| Reto intermedio único | 10–45' | Implementación real en el repo, a partir de `week-XX-start` |
| Validación | 45–55' | Ejecutar tests, verificar pipeline verde, revisión rápida |
| Cierre | 55–60' | Publicar `week-XX-solution`, puntos clave, dudas frecuentes |

### Filosofía del código inicial (`week-XX-start`)

El `week-XX-start` **nunca llega vacío**. Llega con el andamiaje necesario para que el reto quepa en 35 minutos:

| Qué viene dado | Qué hace el participante |
|----------------|--------------------------|
| Proyecto compilando con dependencias correctas | Implementa la lógica del hueco concreto |
| Entidades / interfaces / clases base ya creadas | Completa los métodos vacíos o `// TODO` |
| Tests de andamiaje (compilando, fallando en rojo) | Hace los tests pasar en verde |
| Estructura de paquetes definida | Sigue la convención, no decide la arquitectura base |

**Regla de oro**: si al abrir el `week-XX-start` un participante tarda más de 2 minutos en entender qué tiene que hacer, el start está incompleto.

### Andamiaje por sesión (semanas clave)

| Semana | Qué viene dado en el start |
|--------|---------------------------|
| 03 | `StockValidator` y `OrderNotifier` ya extraídos; falta `DiscountCalculator` y el tipo `LOYALTY` |
| 04 | `ShippingStrategy` + `StandardShipping` ya implementados; faltan `ExpressShipping`, `StorePickup` y `Factory` |
| 10 | `TransferService` con `@Transactional` básico; falta `rollbackFor` y `TransferAuditService` con `REQUIRES_NEW` |
| 12 | Query JPQL sin `Pageable` y entidad con `@Version` ya presente; falta paginación y manejo de `OptimisticLockException` |
| 13 | Proyecto `notification-service` con `pom.xml` y clase `main` creados; falta el endpoint y la integración en el monolito |

### Criterio de aceptación del reto

Cada reto incluye siempre:
1. **1 cambio funcional** — historia de usuario o requerimiento concreto.
2. **1 prueba** — al menos 1 test que valide el comportamiento esperado.
3. **1 criterio no funcional** — calidad, performance, operación o seguridad.

### Escala de madurez esperada

| Seniority | Expectativa |
|-----------|-------------|
| Junior | Implementa los requerimientos funcionales, tests básicos |
| Semi-senior | Aplica principios SOLID, tests significativos |
| Senior | Diseño desacoplado, tests robustos, criterio no funcional cubierto |
| Experto | Identifica trade-offs, propone mejoras, deja el código mejor de como lo encontró |

