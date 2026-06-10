# Criterios de evaluación — Week 12

## Checklist del reviewer

### Paginación
- [ ] Query JPQL con `Pageable` en `ProductRepository`
- [ ] Filtros opcionales funcionan (null → sin filtro)
- [ ] Test verifica `totalElements` y `content.size() <= pageSize`
- [ ] Sin carga de todos los registros en memoria

### Locking optimista
- [ ] `@Version` en entidad `Product`
- [ ] `reserveStock()` maneja `OptimisticLockException`
- [ ] Test de 2 threads concurrentes: solo 1 triunfa

### Calidad
- [ ] Sin `LockModeType.PESSIMISTIC_WRITE`
- [ ] `mvn verify` en verde

## Escala de madurez

| Junior | Semi-senior | Senior | Experto |
|--------|-------------|--------|---------|
| Paginación funcional, @Version presente | Test de concurrencia básico | Specification, @QueryHints | Propone estrategia de locking para el dominio completo (cuándo optimista vs pesimista) |
