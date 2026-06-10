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
