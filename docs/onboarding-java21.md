# Onboarding Java 21 — Guía de configuración

Antes de tu primera sesión, asegurate de tener el entorno configurado correctamente.

---

## 0. Crear cuenta GitHub y hacer fork del repositorio

### 0.1 Crear cuenta GitHub (si no tenés una)
1. Ir a [https://github.com/signup](https://github.com/signup).
2. Elegir un alias identificable (idealmente tu nombre o alias Indra).
3. Completar la verificación y activar la cuenta.

> No es necesario pagar ningún plan. La cuenta **gratuita** es suficiente para todo el programa.

### 0.2 Hacer fork del repositorio central

1. Ir a [https://github.com/robinson8406/java-formation-lab-2026](https://github.com/robinson8406/java-formation-lab-2026).
2. Clic en **Fork** (arriba a la derecha) → **Create fork**.
3. Esto crea una copia en tu cuenta: `https://github.com/tu-alias/java-formation-lab-2026`.

> El fork es **tu espacio de trabajo personal**. No necesitás ningún permiso especial en el repo central.

### 0.3 Clonar tu fork

```bash
git clone https://github.com/tu-alias/java-formation-lab-2026.git
cd java-formation-lab-2026

# Agregar el repo central como "upstream" para traer novedades
git remote add upstream https://github.com/robinson8406/java-formation-lab-2026.git
git remote -v
# origin   https://github.com/tu-alias/java-formation-lab-2026.git (fetch)
# upstream https://github.com/robinson8406/java-formation-lab-2026.git (fetch)
```

### 0.4 Traer las ramas de inicio de cada sesión

```bash
git fetch upstream
git checkout -b week-01/tu-alias upstream/week-01-start
```

---

## 1. Instalar Java 21

### Opción A — SDKMAN (Linux/macOS/WSL)
```bash
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
sdk install java 21.0.3-tem
sdk use java 21.0.3-tem
java -version
```

### Opción B — Winget (Windows)
```powershell
winget install EclipseAdoptium.Temurin.21.JDK
```

### Opción C — Descarga manual
Descargar desde [Adoptium Temurin 21](https://adoptium.net/temurin/releases/?version=21).

---

## 2. Verificar instalación

```bash
java -version
# Debe mostrar: openjdk version "21.x.x"
mvn -version
# Debe mostrar: Apache Maven 3.9.x
```

---

## 3. Configurar el IDE

### IntelliJ IDEA (recomendado)
1. `File → Project Structure → Project SDK` → seleccionar Java 21.
2. `File → Settings → Build → Compiler → Java Compiler` → Target bytecode version: 21.
3. Instalar plugin **SonarLint** para feedback de calidad en tiempo real.

### VS Code
1. Instalar [Extension Pack for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack).
2. En `settings.json`:
   ```json
   "java.configuration.runtimes": [
     { "name": "JavaSE-21", "path": "/ruta/a/jdk-21", "default": true }
   ]
   ```

---

## 4. Verificar que el repo funciona

```bash
# Trae las ramas del repo central
git fetch upstream
git checkout -b week-01/tu-alias upstream/week-01-start
mvn verify
# Debe compilar y ejecutar los tests en verde
```

---

## 6. Docker (requerido desde week-14)

```bash
# Verificar instalación
docker --version
docker compose version
```

Si no tenés Docker instalado: [Docker Desktop](https://www.docker.com/products/docker-desktop/).

---

## 7. Azure CLI (requerido desde week-15)

```bash
# Instalar
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash   # Linux/WSL
winget install Microsoft.AzureCLI                         # Windows

# Verificar
az --version
az login
```

---

## Features de Java 21 que usaremos

| Feature | Uso en el plan |
|---------|---------------|
| Records | DTOs en Spring (week-06) |
| Sealed classes | Jerarquías de dominio (week-03) |
| Pattern matching `instanceof` | Simplificar condicionales |
| Text blocks | Queries JPQL largas (week-12) |
| Virtual threads | Mención en observabilidad (week-18) |

---

## ¿Problemas? 

Abre un issue con el label `configuración` o consulta en el canal del equipo.
