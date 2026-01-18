# 🚀 Setup y Ejecución del Proyecto QA Doctorado 2026

Guía rápida para levantar el SUT (Sistema Bajo Prueba) y comenzar a trabajar.

## ⚡ Quick Start (5 minutos)

### 1. Requisitos Previos
```bash
# Verificar que tienes Docker y Docker Compose
docker --version  # v20.10+
docker-compose --version  # v2.0+
```

### 2. Iniciar el Sistema
```bash
# Navega a la carpeta del proyecto
cd /ruta/al/proyecto

# Ejecuta el script de inicialización
./setup/run_sut.sh
```

### 3. Verificar Que Funciona
```bash
# En otra terminal, ejecuta health check
./setup/healthcheck_sut.sh
```

### 4. Acceder a la API
- **API Base**: http://localhost:8000
- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc

---

## 📦 Componentes

El SUT está compuesto por:

| Componente | Puerto | Status | Check |
|-----------|--------|--------|-------|
| FastAPI App | 8000 | http://localhost:8000 | ✓ |
| PostgreSQL | 5432 | localhost:5432 | ✓ |
| Swagger UI | 8000/docs | http://localhost:8000/docs | ✓ |

---

## 🛠️ Scripts de Utilidad

### `setup/run_sut.sh`
**Inicia el sistema completo**

```bash
# Inicialización normal
./setup/run_sut.sh

# Con reconstrucción de imágenes
./setup/run_sut.sh --rebuild

# Ver ayuda
./setup/run_sut.sh --help
```

### `setup/healthcheck_sut.sh`
**Verifica la salud de todos los componentes**

```bash
# Check básico (rápido)
./setup/healthcheck_sut.sh

# Check detallado (verboso)
./setup/healthcheck_sut.sh --verbose

# Check profundo (incluye tests)
./setup/healthcheck_sut.sh --deep

# Ver ayuda
./setup/healthcheck_sut.sh --help
```

### `setup/stop_sut.sh`
**Detiene el sistema de manera segura**

```bash
# Solo detener (preserva datos)
./setup/stop_sut.sh

# Detener y remover contenedores
./setup/stop_sut.sh --remove

# Limpiar todo incluyendo datos
./setup/stop_sut.sh --volumes

# Ver ayuda
./setup/stop_sut.sh --help
```

---

## 📖 Instalación Paso a Paso

### Paso 1: Clonar el Repositorio
```bash
git clone https://github.com/tu-usuario/fastapi-realworld-qa-doctorado-2026.git
cd fastapi-realworld-qa-doctorado-2026
```

### Paso 2: Configuración Inicial
```bash
# Docker y Docker Compose están instalados?
docker --version
docker-compose --version

# Copiar configuración
cp .env.example .env
```

### Paso 3: Iniciar Servicios
```bash
# Iniciar todo automáticamente
./setup/run_sut.sh

# O manualmente con Docker Compose
docker-compose up -d
docker-compose exec app poetry run alembic upgrade head
```

### Paso 4: Verificar Sistema
```bash
# Health check
./setup/healthcheck_sut.sh

# Ver logs
docker-compose logs -f app
docker-compose logs -f db
```

### Paso 5: Ejecutar Tests
```bash
# Instalar dependencias si no lo hiciste
poetry install

# Ejecutar todos los tests
poetry run pytest

# Ejecutar test específico
poetry run pytest tests/test_api/test_routes/test_users.py -v
```

---

## 🔍 Verificación Posterior

### Confirmar que todo funciona

1. **API respondiendo**:
```bash
curl http://localhost:8000/docs
```

2. **Base de datos conectada**:
```bash
docker-compose exec db psql -U postgres -d rwdb -c "SELECT COUNT(*) FROM users"
```

3. **Tests pasando**:
```bash
poetry run pytest -q
```

Expected output:
```
================================================ 90 passed in ~70s =================================================
```

---

## ❌ Solución de Problemas

### El script no es ejecutable
```bash
chmod +x setup/*.sh
```

### Puerto 8000 ya en uso
```bash
# Opción 1: Liberar el puerto
lsof -i :8000
kill -9 <PID>

# Opción 2: Usar otro puerto en docker-compose.yml
# Editar: ports: ["8001:8000"]
```

### PostgreSQL no inicia
```bash
# Ver logs
docker-compose logs db

# Reiniciar
docker-compose down -v
./setup/run_sut.sh --rebuild
```

### Tests no pasan
```bash
# Health check detallado
./setup/healthcheck_sut.sh --verbose

# Resetear BD
docker-compose exec db psql -U postgres -d rwdb -c "DROP SCHEMA public CASCADE; CREATE SCHEMA public"
docker-compose exec app poetry run alembic upgrade head
```

### Docker no está instalado
```bash
# macOS
brew install docker docker-compose

# Ubuntu/Debian
sudo apt-get install docker.io docker-compose

# Después, agregar usuario al grupo docker
sudo usermod -aG docker $USER
```

---

## 📚 Documentación Completa

- **SUT Selection**: Ver [SUT_SELECTION.md](../SUT_SELECTION.md)
- **Team Agreements**: Ver [AGREEMENTS.md](../AGREEMENTS.md)
- **Setup Scripts**: Ver [setup/README.md](./README.md)
- **Main README**: Ver [README.md](../README.md)

---

## 🎯 Próximos Pasos

Después de iniciar el sistema:

1. **Revisar la Documentación**
   - Lee [AGREEMENTS.md](../AGREEMENTS.md) para entender los acuerdos del equipo
   - Lee [SUT_SELECTION.md](../SUT_SELECTION.md) para entender el SUT

2. **Ejecutar Tests**
   ```bash
   poetry run pytest -v
   ```

3. **Explorar la API**
   - Abre http://localhost:8000/docs
   - Prueba algunos endpoints

4. **Agregar Tus Propios Tests**
   ```bash
   # Crear nuevo test
   mkdir -p tests/my_tests
   touch tests/my_tests/test_mytest.py
   
   # Ejecutar
   poetry run pytest tests/my_tests/ -v
   ```

---

## 🤝 Contribuir

1. Fork el repositorio
2. Crea un branch: `git checkout -b feature/mi-feature`
3. Commit cambios: `git commit -m "feat: descripción"`
4. Push: `git push origin feature/mi-feature`
5. Abre un Pull Request

Ver [AGREEMENTS.md](../AGREEMENTS.md) para más detalles.

---

## ⚙️ Configuración Avanzada

### Variables de Entorno Personalizadas

Editar `.env`:
```bash
# Puerto personalizado
API_PORT=8001

# Nivel de logs
LOG_LEVEL=DEBUG

# Base de datos remota
DATABASE_URL=postgresql://user:pass@remote-host:5432/rwdb
```

### Docker Compose Override

Crear `docker-compose.override.yml`:
```yaml
version: '3.8'
services:
  app:
    ports:
      - "8001:8000"  # Puerto diferente
    environment:
      LOG_LEVEL: DEBUG
  db:
    environment:
      POSTGRES_PASSWORD: mypassword
```

---

## 📋 Checklist Final

Antes de comenzar el proyecto, asegurate que:

- [ ] Docker está instalado: `docker --version`
- [ ] Docker Compose está instalado: `docker-compose --version`
- [ ] Tienes acceso al repositorio
- [ ] Ejecutaste `./setup/run_sut.sh` sin errores
- [ ] `./setup/healthcheck_sut.sh` muestra estado SALUDABLE
- [ ] Puedes acceder a http://localhost:8000/docs
- [ ] Los 90 tests pasan: `poetry run pytest -q`

Si todo esto funciona: **¡Estás listo para comenzar! 🎉**

---

**Última actualización**: Enero 18, 2026  
**Versión**: 1.0.0  
**Estado**: ✅ Listo para usar
