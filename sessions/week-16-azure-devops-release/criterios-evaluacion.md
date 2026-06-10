# Criterios de evaluación — Week 16

## Checklist del reviewer

### Pipeline
- [ ] 3 stages: CI, DeployDev, DeployProd con dependencias correctas
- [ ] `AzureWebApp@1` task configurada en ambos deploy stages
- [ ] Sin credenciales hardcodeadas en el YAML

### Environments
- [ ] Environment `dev` y `prod` definidos en Azure DevOps
- [ ] Aprobación requerida configurada en `prod` (captura de pantalla)
- [ ] Deploy a `dev` automático tras CI verde

### Variables
- [ ] Variable Groups con variables por entorno
- [ ] Service Connection referenciado desde el YAML (no credenciales directas)

### Verificación
- [ ] Deploy exitoso a `dev` (evidencia en el PR)
- [ ] `mvn verify` en verde

## Escala de madurez

| Junior | Semi-senior | Senior | Experto |
|--------|-------------|--------|---------|
| Pipeline con 2 stages, aprobación manual | Variable Groups, 3 stages | Smoke test post-deploy, rollback | Propone estrategia completa: blue-green, feature flags, rollback automático |
