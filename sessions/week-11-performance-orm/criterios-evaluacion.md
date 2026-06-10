# Criterios de evaluación — Week 11

## Checklist del reviewer

### Diagnóstico
- [ ] Logs de SQL habilitados en properties
- [ ] Número de queries antes del fix documentado en el PR

### Fix
- [ ] `JOIN FETCH` implementado en la query JPQL
- [ ] Sin `FetchType.EAGER` añadido como solución
- [ ] Número de queries después: ≤ 3 para el dataset de test

### Test
- [ ] Test con assertion explícita del número de queries (no solo "pasa")
- [ ] `mvn verify` en verde

### Calidad
- [ ] La query funciona con paginación (no rompe `Pageable`)
- [ ] Sin consultas N+1 residuales en otros métodos del repositorio

## Escala de madurez

| Junior | Semi-senior | Senior | Experto |
|--------|-------------|--------|---------|
| JOIN FETCH básico, sin métricas | Test con conteo de queries | @EntityGraph alternativo, batch_fetch_size | Propone estrategia de detección de N+1 en CI (Datasource proxy, p6spy) |
