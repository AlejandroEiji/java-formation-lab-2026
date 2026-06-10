# Criterios de evaluación — Week 07

## Checklist del reviewer

### Profiles
- [ ] `@Profile("dev")` en `FakeEmailSender`
- [ ] `@Profile("prod")` en `SmtpEmailSender`
- [ ] Ambos beans no están activos simultáneamente

### Wiring
- [ ] `NotificationService` usa inyección por constructor
- [ ] Sin `@Autowired` en ningún campo de las clases nuevas o modificadas
- [ ] Sin `if` de entorno en el código de negocio

### Configuración
- [ ] `application-dev.properties` y `application-prod.properties` presentes
- [ ] Al menos una propiedad diferente entre perfiles

### Tests
- [ ] Test con `@ActiveProfiles("dev")` verificando que `FakeEmailSender` es el bean activo
- [ ] `mvn verify` en verde sin conexión de red

## Escala de madurez

| Junior | Semi-senior | Senior | Experto |
|--------|-------------|--------|---------|
| Profiles básicos, inyección por constructor | Properties por entorno, test con @ActiveProfiles | @ConditionalOnProperty, @TestConfiguration, sin rastro de if de entorno | Propone estrategia de configuración para todos los entornos del proyecto |
