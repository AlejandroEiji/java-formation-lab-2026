# Enunciado — Week 15: Azure DevOps Pipelines (CI)

## Contexto del reto

El equipo de **Indra Retail** mergea código directamente a `main` sin validación automática. La semana pasada, un PR con tests rotos llegó a producción porque nadie los ejecutó localmente. Tu tarea es crear un pipeline CI que impida que eso vuelva a ocurrir.

## Lo que debes implementar

Crea `azure-pipelines.yml` en la raíz del proyecto con:

### Trigger
```yaml
trigger:
  branches:
    include:
      - main
pr:
  branches:
    include:
      - main
```

### Stage 1: Build & Test
```yaml
stages:
  - stage: CI
    jobs:
      - job: BuildAndTest
        pool:
          vmImage: ubuntu-latest
        steps:
          - task: JavaToolInstaller@0
            inputs:
              versionSpec: '21'
              jdkArchitectureOption: x64
              jdkSourceOption: PreInstalled
          - task: Cache@2
            inputs:
              key: 'maven | $(Agent.OS) | pom.xml'
              path: $(HOME)/.m2/repository
          - script: mvn verify --no-transfer-progress
            displayName: 'Build & Test'
          - task: PublishTestResults@2
            inputs:
              testResultsFormat: JUnit
              testResultsFiles: '**/surefire-reports/TEST-*.xml'
            condition: always()
          - task: PublishCodeCoverageResults@2
            inputs:
              summaryFileLocation: '**/jacoco.xml'
              reportDirectory: '**/site/jacoco'
```

### Quality Gate
Agrega un step que falle el pipeline si la cobertura es inferior al 70%:
```yaml
          - script: |
              COVERAGE=$(grep -oP 'missed="\K[0-9]+(?="[^/]*/>' target/site/jacoco/jacoco.xml | head -1)
              echo "Verificando quality gate de cobertura..."
              mvn verify -Djacoco.check.coveredRatio=0.70
            displayName: 'Quality Gate: Cobertura >= 70%'
```

Configura `jacoco-maven-plugin` en el `pom.xml` con el check de cobertura mínima.

## Restricciones técnicas (para todos)

- El pipeline debe ejecutar en `ubuntu-latest` — sin agentes self-hosted por ahora.
- El cache de Maven debe estar configurado para no descargar dependencias en cada ejecución.
- **Criterio no funcional (operación)**: el pipeline debe completar en menos de 5 minutos.

## Criterio de aceptación del PR

- [ ] `azure-pipelines.yml` presente en la raíz
- [ ] Pipeline verde en Azure DevOps (captura de pantalla en el PR)
- [ ] Resultados de tests publicados en la UI de Azure DevOps
- [ ] Quality gate de cobertura configurado en `pom.xml`
- [ ] Cache de Maven configurado
- [ ] `mvn verify` en verde localmente

## Bonus (opcional)

- Configurar branch policies en Azure DevOps para bloquear el merge si el pipeline falla.
- Agregar un step de análisis estático con Checkstyle o SpotBugs.
