# Criterios de evaluación — Week 15

## Checklist del reviewer

### Pipeline YAML
- [ ] `azure-pipelines.yml` en la raíz del proyecto
- [ ] Trigger para `main` y PR hacia `main`
- [ ] `JavaToolInstaller` con versión 21
- [ ] Cache de Maven configurado correctamente

### Build & Test
- [ ] `mvn verify` ejecutado en el pipeline
- [ ] `PublishTestResults` configurado
- [ ] Pipeline verde (captura de pantalla en el PR)

### Quality Gate
- [ ] `jacoco-maven-plugin` con check de cobertura mínima en `pom.xml`
- [ ] Pipeline falla si la cobertura < 70%

### Performance
- [ ] Pipeline completa en < 5 minutos (reportar tiempo en el PR)

## Escala de madurez

| Junior | Semi-senior | Senior | Experto |
|--------|-------------|--------|---------|
| Pipeline verde, tests publicados | Cache de Maven, quality gate | Branch policies, Checkstyle | Propone estrategia de pipeline completa: CI + CD + rollback automático |
