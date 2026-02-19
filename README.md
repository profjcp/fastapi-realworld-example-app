# QA Doctorado 2026 - Equipo X

## Descripción del Proyecto

Este repositorio contiene todo el trabajo y documentación para el proyecto **QA Doctorado 2026** del **Equipo X**.

Es un **System Under Test (SUT)** basado en FastAPI RealWorld - una aplicación completa de ejemplo que implementa la especificación Conduit con arquitectura moderna de FastAPI, incluyendo autenticación JWT, base de datos PostgreSQL y suite completa de pruebas.

## 🚀 Características Principales

- **API RESTful**: 90+ endpoints implementados
- **Autenticación**: JWT con cifrado seguro
- **Base de Datos**: PostgreSQL con migraciones Alembic
- **Testing**: 90 tests automatizados con cobertura completa
- **Documentación**: Swagger UI y ReDoc integrados
- **CI/CD Ready**: Configuración para integración continua

## 📁 Estructura del Repositorio

```
.
├── setup/              - Scripts de configuración del entorno
├── scripts/            - Scripts de pruebas y mediciones
├── evidence/           - Recolección de evidencias semanales
├── quality/            - Escenarios de calidad y glosario
├── risk/               - Evaluación de riesgos y estrategia de pruebas
├── design/             - Diseño de casos de prueba y reglas de oráculo
├── ci/                 - Configuración de integración continua
├── memos/              - Memorandums de progreso semanal
├── reports/            - Reportes de unidad
├── study/              - Materiales del estudio de investigación
├── paper/              - Paper final
├── slides/             - Materiales de presentación
├── peer_review/        - Materiales de revisión por pares
├── app/                - Código fuente de la aplicación FastAPI
├── tests/              - Suite completa de pruebas (90 tests)
├── Dockerfile          - Configuración Docker
├── docker-compose.yml  - Orquestación de contenedores
└── README.md           - Este archivo
```

## 🧪 Testing & QA

### Estructura de QA

- Matriz de riesgos y estrategia: risk/
- Evidencia y RUNLOGs: evidence/
- Escenarios de calidad: quality/

### Semana 5 - Quality Gate

- Definicion del gate: ci/quality_gates.md
- Ejecutor local/CI: bash ci/run_quality_gate.sh
- Evidencia generada: evidence/week5/

### Ejecutar pruebas

**Script de pruebas con cobertura:**

```bash
./scripts/test
```

**Pytest directo:**

```bash
poetry run pytest -v --cov=app --cov=tests --cov-report=term-missing
```

### Ver evidencia

```bash
ls -la evidence/week3/
cat evidence/week3/RUNLOG.md
```

## ⚡ Primeros Pasos

### 1. Revisar Acuerdos de Equipo
Consulta el archivo de acuerdos de equipo en la sección **Agreements** del wiki del repositorio.

### 2. Requisitos Previos

- **Python 3.8+** (Recomendado: 3.11+)
- **Poetry** - Gestor de dependencias
- **Docker** y **Docker Compose**
- **PostgreSQL** 12+ (vía Docker)

### 3. Instalación Rápida

#### Opción A: Con Docker (Recomendado)

```bash
# Clonar el repositorio
git clone <URL_DEL_REPOSITORIO>
cd fastapi-realworld-example-app

# Levantar la aplicación y BD
docker-compose up -d
```

La aplicación estará disponible en: **http://localhost:8000**

#### Opción B: Instalación Local

```bash
# 1. Instalar Poetry (si no lo tienes)
curl -sSL https://install.python-poetry.org | python3 -

# 2. Clonar y configurar
git clone <URL_DEL_REPOSITORIO>
cd fastapi-realworld-example-app
poetry install

# 3. Configurar variables de entorno
cp .env.example .env
# Editar .env con tus valores

# 4. Levantar PostgreSQL
export POSTGRES_DB=rwdb POSTGRES_PORT=5432 POSTGRES_USER=postgres POSTGRES_PASSWORD=postgres
docker run --name pgdb --rm -d -e POSTGRES_USER="$POSTGRES_USER" -e POSTGRES_PASSWORD="$POSTGRES_PASSWORD" \
  -e POSTGRES_DB="$POSTGRES_DB" -p 5432:5432 postgres

# 5. Ejecutar migraciones
poetry run alembic upgrade head

# 6. Iniciar la aplicación
poetry run uvicorn app.main:app --reload
```

## 📊 Ejecución del Proyecto

### Ver Comandos Disponibles

```bash
# Si tienes make instalado
make

# Si no tienes make, consulta los scripts en setup/
ls -la setup/
```

### Correr la Aplicación

```bash
poetry run uvicorn app.main:app --reload
```

**Acceso a la API:**
- Swagger UI: http://localhost:8000/docs
- ReDoc: http://localhost:8000/redoc
- API Base: http://localhost:8000/api

### Ejecutar Pruebas

```bash
# Todos los tests
poetry run pytest -v

# Con reporte de cobertura
poetry run pytest --cov=app --cov-report=html

# Test específico
poetry run pytest tests/test_api/test_routes/test_users.py -v

# Tests sin output verbose
poetry run pytest -q
```

## 🧪 Suite de Pruebas

- **Total de Tests**: 90
- **Cobertura**: Completa (API, DB, Servicios, Modelos)
- **Framework**: pytest + pytest-asyncio
- **Tiempo de ejecución**: ~70 segundos

### Categorías de Pruebas

```
tests/
├── test_api/
│   ├── test_errors/          - Manejo de errores (HTTP 422, 404, etc)
│   └── test_routes/          - Pruebas de endpoints
│       ├── test_articles.py  - 31 tests
│       ├── test_authentication.py
│       ├── test_comments.py
│       ├── test_login.py
│       ├── test_profiles.py
│       ├── test_registration.py
│       ├── test_tags.py
│       └── test_users.py     - 20 tests
├── test_db/
│   └── test_queries/         - Pruebas de base de datos
├── test_schemas/             - Validación de modelos Pydantic
└── test_services/            - Pruebas de servicios (JWT, seguridad)
```

## 🔧 Configuración

### Variables de Entorno (.env)

```bash
APP_ENV=dev
DATABASE_URL=postgresql://postgres:postgres@127.0.0.1:5432/rwdb
SECRET_KEY=tu-clave-secreta-aqui-cambiar-en-produccion
```

### Configuración de PostgreSQL

La aplicación usa PostgreSQL como base de datos principal. Puedes:

- **Levantar con Docker**: `docker run -d --name pgdb -p 5432:5432 postgres`
- **Usar PostgreSQL local**: Asegurar que el `DATABASE_URL` apunte correctamente

## 📝 Estructura de la Aplicación

```
app/
├── main.py              - Punto de entrada de FastAPI
├── api/
│   ├── routes/          - Definición de endpoints
│   ├── dependencies/    - Inyección de dependencias
│   └── errors/          - Manejo de errores HTTP
├── core/
│   ├── config.py        - Configuración global
│   ├── settings/        - Configuraciones por entorno
│   └── logging.py       - Sistema de logs
├── db/
│   ├── repositories/    - CRUD operations
│   ├── migrations/      - Migraciones Alembic
│   └── queries/         - Queries SQL
├── models/
│   ├── domain/          - Modelos de dominio
│   └── schemas/         - Esquemas Pydantic (validación)
├── services/            - Lógica de negocio
│   ├── jwt.py           - Manejo de tokens JWT
│   └── security.py      - Funciones de seguridad
└── resources/           - Strings y constantes
```

## 👥 Miembros del Equipo

| Nombre | Rol | Contacto |
|--------|-----|----------|
| [Miembro 1] | Líder | [Email/GitHub] |
| [Miembro 2] | Ingeniero QA | [Email/GitHub] |
| [Miembro 3] | Ingeniero QA | [Email/GitHub] |
| [Miembro 4] | Soporte | [Email/GitHub] |

*Actualizar con los nombres y roles reales del equipo*

## 📚 Documentación Adicional

- [API Specification](./docs/API.md) - Especificación de endpoints
- [Test Plan](./design/test_plan.md) - Plan de pruebas
- [Risk Assessment](./risk/risk_assessment.md) - Evaluación de riesgos
- [Weekly Progress](./memos/) - Memorandums de progreso semanal

## 🐛 Solución de Problemas

### Error de Conexión a PostgreSQL

```
sqlalchemy.exc.OperationalError: could not connect to server
```

**Solución**: Verificar que PostgreSQL está corriendo y el `DATABASE_URL` es correcto:

```bash
# Verificar contenedor Docker
docker ps | grep pgdb

# Restaurar conexión
export DATABASE_URL=postgresql://postgres:postgres@127.0.0.1:5432/rwdb
```

### Tests Fallando

```bash
# Limpiar cache y reinstalar
poetry cache clear . --all
poetry install --no-cache
```

### Puerto 8000 ya en uso

```bash
# Cambiar puerto
poetry run uvicorn app.main:app --port 8001 --reload
```

## 🚀 Deployment

### Con Docker Compose

```bash
# Iniciar todos los servicios
docker-compose up -d

# Ver logs
docker-compose logs -f app

# Detener
docker-compose down
```

### Con Kubernetes (Opcional)

Revisar configuración en `ci/kubernetes/` para deployment en producción.

## 📋 Checklist de Configuración

- [ ] Clonar repositorio
- [ ] Instalar Python 3.8+ y Poetry
- [ ] Instalar Docker y Docker Compose
- [ ] Ejecutar `poetry install`
- [ ] Configurar archivo `.env`
- [ ] Levantar PostgreSQL
- [ ] Ejecutar migraciones: `poetry run alembic upgrade head`
- [ ] Verificar app en http://localhost:8000/docs
- [ ] Ejecutar tests: `poetry run pytest`
- [ ] Confirmar que todos los 90 tests pasan ✅

## 📖 Referencias

- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [Realworld Spec](https://realworld.io/)
- [pytest Documentation](https://docs.pytest.org/)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)

## 📄 Licencia

Este proyecto es parte del programa de **QA Doctorado 2026** y está bajo licencia MIT.

---

**Última actualización**: Enero 2026  
**Versión de la API**: 1.0.0  
**Estado**: En desarrollo activo ✅
