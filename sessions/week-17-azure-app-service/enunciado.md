# Enunciado — Week 17: Azure App Service

## Contexto del reto

**Indra Retail** necesita desplegar su API en Azure de forma controlada. Actualmente la conexión a la base de datos está hardcodeada en `application.properties`, el deploy requiere downtime de 5 minutos y cuando algo falla en producción no saben dónde buscar los logs.

## Lo que debes implementar

### 1. Crear la infraestructura (Azure CLI)

```bash
# Resource Group
az group create --name rg-indra-retail-dev --location eastus

# App Service Plan (Free tier para la sesión)
az appservice plan create \
  --name plan-indra-retail \
  --resource-group rg-indra-retail-dev \
  --sku F1 \
  --is-linux

# App Service
az webapp create \
  --name indra-retail-<tu-alias> \
  --resource-group rg-indra-retail-dev \
  --plan plan-indra-retail \
  --runtime "JAVA:21-java21"

# Deployment slot (staging)
az webapp deployment slot create \
  --name indra-retail-<tu-alias> \
  --resource-group rg-indra-retail-dev \
  --slot staging
```

### 2. Configurar Application Settings (secretos fuera del código)

```bash
az webapp config appsettings set \
  --name indra-retail-<tu-alias> \
  --resource-group rg-indra-retail-dev \
  --settings \
    SPRING_DATASOURCE_URL="jdbc:postgresql://..." \
    SPRING_DATASOURCE_USERNAME="@Microsoft.KeyVault(...)" \
    SPRING_PROFILES_ACTIVE="prod"
```

### 3. Desplegar al slot staging y hacer swap

```bash
# Deploy al slot staging
az webapp deploy \
  --name indra-retail-<tu-alias> \
  --resource-group rg-indra-retail-dev \
  --slot staging \
  --src-path target/app.jar \
  --type jar

# Verificar staging
curl https://indra-retail-<tu-alias>-staging.azurewebsites.net/actuator/health

# Swap staging → production (zero downtime)
az webapp deployment slot swap \
  --name indra-retail-<tu-alias> \
  --resource-group rg-indra-retail-dev \
  --slot staging \
  --target-slot production
```

### 4. Habilitar logs y troubleshooting

```bash
# Habilitar logging de aplicación
az webapp log config \
  --name indra-retail-<tu-alias> \
  --resource-group rg-indra-retail-dev \
  --application-logging filesystem \
  --level information

# Stream de logs en tiempo real
az webapp log tail \
  --name indra-retail-<tu-alias> \
  --resource-group rg-indra-retail-dev
```

### 5. Documenta en el PR

- URL de la app desplegada.
- Screenshot de `GET /actuator/health` respondiendo desde Azure.
- Screenshot de Application Settings en el portal (sin mostrar valores de secretos).

## Restricciones técnicas (para todos)

- **Sin credenciales en el código** — todo a través de Application Settings.
- La URL de la base de datos no debe aparecer en ningún archivo del repo.
- **Criterio no funcional (seguridad)**: las credenciales deben gestionarse como Application Settings o Key Vault references — nunca como variables de entorno en el Dockerfile.

## Criterio de aceptación del PR

- [ ] App desplegada y respondiendo en Azure (URL en el PR)
- [ ] `GET /actuator/health` retorna 200 desde Azure
- [ ] Sin credenciales en ningún archivo del repo
- [ ] Deployment slot `staging` configurado
- [ ] Swap staging → production ejecutado exitosamente
- [ ] Logs de aplicación accesibles

## Bonus (opcional)

- Referenciar secretos desde Azure Key Vault usando `@Microsoft.KeyVault(...)` en Application Settings.
- Configurar Auto-swap automático al deploy exitoso en staging.
