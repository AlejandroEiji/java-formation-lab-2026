# Criterios de evaluación — Week 09

## Checklist del reviewer

### Mapeos
- [ ] 4 entidades presentes con los campos requeridos
- [ ] `@ManyToOne(fetch = LAZY)` en todas las relaciones
- [ ] Sin `FetchType.EAGER` sin justificación
- [ ] Sin `cascade = ALL` sin justificación
- [ ] `orphanRemoval = true` en Order → OrderItem

### Restricciones de base de datos
- [ ] `@Column(nullable = false)` en campos obligatorios
- [ ] `@Column(unique = true)` en email de Customer
- [ ] Llaves foráneas correctamente definidas con `@JoinColumn`

### Tests
- [ ] Test que carga Order con ítems en una transacción activa (sin LazyInitializationException)
- [ ] `mvn verify` en verde (Flyway o H2 configurado)

### Calidad
- [ ] El modelo hace imposible guardar un OrderItem sin Order
- [ ] Nombres de tablas y columnas coherentes (snake_case)

## Escala de madurez

| Junior | Semi-senior | Senior | Experto |
|--------|-------------|--------|---------|
| Mapeos funcionales, algunos EAGER | LAZY en todo, cascade correcto | @Version, @Embeddable, test robusto | Propone el esquema DDL completo y justifica cada decisión de cascade |
