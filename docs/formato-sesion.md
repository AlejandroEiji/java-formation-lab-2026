# Formato de sesión

Cada sesión dura **1 hora**, se realiza **cada jueves** y sigue este formato fijo:

| Segmento | Tiempo | Responsable | Contenido |
|----------|--------|-------------|-----------|
| Contexto + demo | 0–10' | Formador | Qué vamos a mejorar, por qué importa, demo rápida del código inicial |
| Reto intermedio único | 10–45' | Participante | Implementación real en el repo, a partir de `week-XX-start` |
| Validación | 45–55' | Todos | Ejecutar tests, verificar pipeline verde, revisión rápida de soluciones |
| Cierre | 55–60' | Formador | Publicación de `week-XX-solution`, puntos clave, dudas frecuentes |

---

## Definición del reto intermedio

El reto de cada sesión cumple siempre esta estructura mínima:

1. **1 cambio funcional** — una historia de usuario o requerimiento concreto que implementar.
2. **1 prueba** — al menos 1 test que valide el comportamiento esperado.
3. **1 criterio no funcional** — elegido entre:
   - **Calidad**: diseño limpio, SOLID, cobertura
   - **Performance**: tiempo de respuesta, consultas eficientes
   - **Operación**: logs, health, métricas
   - **Seguridad**: validación de input, datos sensibles

Esto garantiza que el reto no sea "solo codear" y que haya diferenciación real entre seniorities.

---

## Filosofía de niveles

| Seniority | Expectativa en el reto |
|-----------|----------------------|
| Junior | Implementa los requerimientos funcionales, tests básicos |
| Semi-senior | Aplica principios SOLID, tests significativos |
| Senior | Diseño desacoplado, tests robustos, criterio no funcional cubierto |
| Experto | Identifica trade-offs, propone mejoras, deja el código mejor de como lo encontró |

---

## Ramas por sesión

```
week-XX-start     ← código con el problema a resolver (publicado antes del jueves)
week-XX-solution  ← solución de referencia (publicada al cerrar la sesión, min 55')
week-XX/<alias>   ← tu entrega personal (PR hacia week-XX-start)
```

---

## Filosofía del código inicial (`week-XX-start`)

El `week-XX-start` **nunca llega vacío**. Llega con el andamiaje necesario para que el reto quepa en 35 minutos de implementación real:

| Qué viene dado en `week-XX-start` | Qué hace el participante |
|-----------------------------------|--------------------------|
| Proyecto compilando con dependencias correctas | Implementa la lógica del hueco concreto |
| Entidades / interfaces / clases base ya creadas | Completa los métodos vacíos o `// TODO` |
| Tests de andamiaje (compilando, fallando en rojo) | Hace los tests pasar en verde |
| Estructura de paquetes definida | Sigue la convención, no decide la arquitectura base |

**Regla de oro**: si al abrir el `week-XX-start` un participante tarda más de 2 minutos en entender qué tiene que hacer, el start está incompleto.

### Sesiones con andamiaje especialmente importante

| Semana | Qué viene dado en el start |
|--------|---------------------------|
| 03 | `StockValidator` y `OrderNotifier` ya extraídos; falta `DiscountCalculator` y el tipo `LOYALTY` |
| 04 | `ShippingStrategy` + `StandardShipping` ya implementados; faltan `ExpressShipping`, `StorePickup` y `Factory` |
| 10 | `TransferService` con `@Transactional` básico; falta `rollbackFor` y `TransferAuditService` con `REQUIRES_NEW` |
| 12 | Query JPQL sin `Pageable` y entidad con `@Version` ya presente; falta paginación y manejo de `OptimisticLockException` |
| 13 | Proyecto `notification-service` con `pom.xml` y clase `main` creados; falta el endpoint y la integración en el monolito |

---

## Pipeline de validación

Cada `week-XX-start` tiene configurado un pipeline de CI que ejecuta:

```
mvn verify
```

El PR **no puede mergearse** si el pipeline falla. Esto garantiza que nadie entregue código roto.
