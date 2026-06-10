# Criterios de evaluación — Week 17

## Checklist del reviewer

### Infraestructura
- [ ] App Service creado en Azure (URL en el PR)
- [ ] Deployment slot `staging` configurado
- [ ] App Service Plan con runtime Java 21

### Seguridad
- [ ] Sin credenciales en ningún archivo del repo (verificar con grep)
- [ ] Application Settings configurados con variables de entorno
- [ ] `SPRING_PROFILES_ACTIVE=prod` configurado

### Deploy
- [ ] App desplegada en slot `staging`
- [ ] Swap staging → production ejecutado
- [ ] `GET /actuator/health` desde Azure retorna 200 (captura en el PR)

### Observabilidad
- [ ] Logging de aplicación habilitado
- [ ] Se puede hacer `az webapp log tail` (demostrado en sesión o captura)

## Escala de madurez

| Junior | Semi-senior | Senior | Experto |
|--------|-------------|--------|---------|
| App desplegada, health check verde | Deployment slots, Application Settings | Key Vault references, Auto-swap | Propone arquitectura: App Service + Front Door + WAF + Application Insights |
