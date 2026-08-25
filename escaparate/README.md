# Escaparate — distribución integrada

Aplicación didáctica preparada para actividades de despliegue.

En esta distribución el **frontend y la API Spring Boot se sirven juntos** desde la misma aplicación. PostgreSQL se ejecuta como servicio independiente.

```text
Navegador
    ↓
Escaparate
├── frontend
└── API Spring Boot
      ↓
 PostgreSQL
```

## Requisitos

- Java 21
- Docker y Docker Compose

## Arranque local

Levanta PostgreSQL:

```powershell
docker compose -f compose.dev.yaml up -d
```

Arranca la aplicación:

```powershell
.\mvnw.cmd spring-boot:run
```

Abre:

```text
http://localhost:8080
```

PostgreSQL se publica en `localhost:15432` para evitar conflictos con instalaciones locales que utilicen `5432`.

## Validación

```powershell
.\mvnw.cmd clean verify
```

La validación ejecuta los tests, genera el WAR, comprueba la cobertura JaCoCo y genera Javadoc.

Artefactos principales:

```text
target/escaparate.war
target/frontend-static/
target/site/jacoco/index.html
target/javadoc/apidocs/index.html
```

## Endpoints útiles para despliegue

```text
GET /api/productos
GET /api/instancia
GET /api/salud/vivo
GET /api/salud/listo
GET /api/carga?ms=1000
```

- `/api/instancia`: identifica la instancia que responde.
- `/api/salud/vivo`: comprueba que el proceso está vivo.
- `/api/salud/listo`: comprueba que la aplicación está preparada para recibir tráfico y que PostgreSQL responde.
- `/api/carga`: genera carga de CPU de forma controlada.

## Configuración por entorno

| Variable | Valor por defecto |
| --- | --- |
| `DB_HOST` | `localhost` |
| `DB_PORT` | `15432` |
| `DB_NAME` | `escaparate` |
| `DB_USER` | `escaparate` |
| `DB_PASSWORD` | `escaparate` |
| `APP_STORAGE_TYPE` | `filesystem` |
| `APP_STORAGE_PATH` | `./uploads` |
| `APP_INSTANCE_NAME` | hostname del sistema |
| `APP_HEALTH_DB_TIMEOUT_SECONDS` | `2` |
| `APP_LOAD_MAX_MS` | `5000` |
| `SERVER_PORT` | `8080` |

## Nota

Trabaja únicamente con los ficheros y requisitos indicados en la actividad. No necesitas conocer otras variantes de Escaparate.
