# Enunciado — Week 16: Azure DevOps Release

## Contexto del reto

El equipo de **Indra Retail** despliega a producción manualmente: copian el JAR por SSH, reinician el proceso y rezan para que funcione. No hay control de qué versión está en cada entorno, no hay aprobación antes de prod y el rollback es manual. Tu tarea es implementar un release pipeline que resuelva eso.

## Lo que debes implementar

Extiende el `azure-pipelines.yml` de la semana anterior con stages de deploy:

### Stage: Deploy to Dev
```yaml
  - stage: DeployDev
    dependsOn: CI
    condition: succeeded()
    jobs:
      - deployment: DeployToDev
        environment: dev
        strategy:
          runOnce:
            deploy:
              steps:
                - script: echo "Desplegando versión $(Build.BuildNumber) en DEV"
                - task: AzureWebApp@1
                  inputs:
                    azureSubscription: '$(AZURE_SERVICE_CONNECTION)'
                    appName: '$(APP_NAME_DEV)'
                    package: '$(Pipeline.Workspace)/**/*.jar'
```

### Stage: Deploy to Prod
```yaml
  - stage: DeployProd
    dependsOn: DeployDev
    condition: succeeded()
    jobs:
      - deployment: DeployToProd
        environment: prod     # ← environment con aprobación requerida en Azure DevOps
        strategy:
          runOnce:
            deploy:
              steps:
                - script: echo "Desplegando versión $(Build.BuildNumber) en PROD"
                - task: AzureWebApp@1
                  inputs:
                    azureSubscription: '$(AZURE_SERVICE_CONNECTION)'
                    appName: '$(APP_NAME_PROD)'
                    package: '$(Pipeline.Workspace)/**/*.jar'
```

### Variables por entorno
Crea grupos de variables en Azure DevOps Library:
- `vars-dev`: `APP_NAME_DEV`, `SPRING_DATASOURCE_URL` (apuntando a BD dev)
- `vars-prod`: `APP_NAME_PROD`, `SPRING_DATASOURCE_URL` (apuntando a BD prod)

### Configurar aprobación en el environment `prod`
En Azure DevOps UI: `Environments → prod → Approvals and checks → Add approval`.

## Restricciones técnicas (para todos)

- Las credenciales de Azure deben estar en un **Service Connection** — nunca en el YAML.
- Las URLs y nombres de app por entorno deben estar en **Variable Groups**, no hardcodeadas.
- **Criterio no funcional (operación)**: el deploy a `prod` debe requerir aprobación explícita de al menos 1 persona.

## Criterio de aceptación del PR

- [ ] `azure-pipelines.yml` con 3 stages: CI → DeployDev → DeployProd
- [ ] Deploy a `dev` automático tras CI verde
- [ ] Deploy a `prod` requiere aprobación (captura de pantalla de la configuración)
- [ ] Variables en Variable Groups, no hardcodeadas en YAML
- [ ] `mvn verify` en verde

## Bonus (opcional)

- Agregar un smoke test post-deploy que verifique `GET /actuator/health` antes de marcar el deploy como exitoso.
- Configurar rollback automático si el smoke test falla.
