# Enunciado — Week 14: Docker + Compose

## Contexto del reto

El equipo de **Indra Retail** tiene problemas de onboarding: cada nuevo desarrollador tarda 2 horas en configurar el entorno local (Java, Postgres, variables de entorno, migraciones). Tu tarea es dockerizar la aplicación para que cualquiera pueda levantar el entorno completo con `docker compose up`.

## Lo que debes implementar

### 1. Dockerfile multi-stage

```dockerfile
# Stage 1: Build
FROM eclipse-temurin:21-jdk AS builder
WORKDIR /app
COPY .mvn .mvn
COPY mvnw pom.xml ./
RUN ./mvnw dependency:go-offline
COPY src ./src
RUN ./mvnw package -DskipTests

# Stage 2: Runtime
FROM eclipse-temurin:21-jre AS runtime
WORKDIR /app
RUN addgroup --system appgroup && adduser --system --ingroup appgroup appuser
USER appuser
COPY --from=builder /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
```

Ajusta según el proyecto del `week-14-start`.

### 2. docker-compose.yml

Crea `docker-compose.yml` con:
- Servicio `app`: construye desde el Dockerfile, espera a que `db` esté healthy.
- Servicio `db`: imagen `postgres:16-alpine`, con `POSTGRES_DB`, `POSTGRES_USER`, `POSTGRES_PASSWORD` en variables de entorno.
- Health check en `db`: `pg_isready`.
- Volumen persistente para los datos de Postgres.
- Red interna `app-network`.

### 3. Variables de entorno

- Crea `.env.example` con las variables requeridas (sin valores reales).
- Agrega `.env` al `.gitignore`.
- La app debe leer `SPRING_DATASOURCE_URL`, `SPRING_DATASOURCE_USERNAME`, `SPRING_DATASOURCE_PASSWORD` desde el entorno.

### 4. Verificación

Documenta en el PR:
```bash
docker compose up --build
# La app debe responder en http://localhost:8080/actuator/health
```

## Restricciones técnicas (para todos)

- La imagen final (`runtime`) no debe contener el JDK — solo JRE.
- El contenedor no debe correr como `root`.
- Las credenciales de base de datos **nunca** en el `Dockerfile` ni en `docker-compose.yml` directamente.
- **Criterio no funcional (seguridad)**: usuario no-root, sin secretos hardcodeados en imágenes.

## Criterio de aceptación del PR

- [ ] Dockerfile multi-stage: imagen final < 300MB
- [ ] `docker compose up` levanta app + db correctamente
- [ ] Health check en el servicio `db`
- [ ] `.env.example` presente, `.env` en `.gitignore`
- [ ] App no corre como root
- [ ] `mvn verify` en verde

## Bonus (opcional)

- Agregar un servicio `adminer` o `pgadmin` al compose para explorar la base de datos.
- Configurar `JAVA_OPTS` en el compose para limitar el heap de la JVM.
