# Changelog - QA Doctorado 2026

Todos los cambios notables a este proyecto se documentarán en este archivo.

El formato está basado en [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
y este proyecto adhiere a [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.0.0] - 2026-01-18

### 🎉 Initial Release - QA Doctorado Setup

#### Added (Nuevas Características)
- ✅ Documentación completa del SUT (SUT_SELECTION.md)
- ✅ Acuerdos de equipo (AGREEMENTS.md)
- ✅ Guía de setup (SETUP.md)
- ✅ README.md con documentación del proyecto
- ✅ Script de inicialización: `setup/run_sut.sh`
- ✅ Script de detención: `setup/stop_sut.sh`
- ✅ Script de health check: `setup/healthcheck_sut.sh`
- ✅ Configuración con pytest.ini actualizado
- ✅ Actualización de dependencias críticas (bcrypt)
- ✅ Archivo .env.example para configuración

#### Changed (Cambios)
- 🔄 Actualizado bcrypt a versión 5.0.0 para compatibilidad con Python 3.11
- 🔄 Actualizado pytest.ini para asincio mode automático
- 🔄 Mejorada documentación del README original (README.rst)
- 🔄 Actualizado poetry.lock con dependencias resueltas

#### Fixed (Correcciones)
- 🐛 Resuelto problema de compatibilidad de pytest-cov con pytest 7.4.4
- 🐛 Corregida configuración de asyncio para tests
- 🐛 Resuelto error de validación de contraseña en bcrypt

#### Deprecated (Deprecaciones)
- ⚠️ Nota: poetry.dev-dependencies será removido en futuras versiones de Poetry

#### Security (Seguridad)
- 🔒 Agregado .env.example (sin credenciales reales)
- 🔒 Documentados mejores prácticas de seguridad en AGREEMENTS.md

---

## Estructura de Versiones Futuras

### [1.1.0] - Q1 2026
- [ ] Agregar tests adicionales para cobertura 100%
- [ ] Integración con CI/CD (GitHub Actions)
- [ ] Documentación de casos de prueba adicionales
- [ ] Métricas de calidad

### [1.2.0] - Q2 2026
- [ ] API documentation mejorada
- [ ] Performance benchmarks
- [ ] Load testing scripts
- [ ] Reportes automatizados

### [2.0.0] - Q3 2026
- [ ] Nuevas características del SUT
- [ ] Cambios arquitectónicos mayores
- [ ] Migración a FastAPI 1.0 (si aplica)

---

## Guía de Contribución

Para agregar cambios al changelog:

1. Edita este archivo en tu rama
2. Agrega nueva sección [X.Y.Z] arriba de [Unreleased]
3. Categoriza cambios: Added, Changed, Fixed, Deprecated, Removed, Security
4. Incluye emojis para claridad visual
5. Usa viñetas con - para sub-items

### Formato de Commit

```
## [X.Y.Z] - YYYY-MM-DD

### Added
- ✅ Nueva funcionalidad 1
- ✅ Nueva funcionalidad 2

### Fixed
- 🐛 Bugfix 1
```

---

## Cómo Leer Este Archivo

**Para usuarios finales**: Lee las secciones "Added" y "Fixed" para entender qué cambió

**Para desarrolladores**: Lee todas las secciones para entender cambios profundos

**Para DevOps**: Lee "Security" y cambios en scripts/configuración

---

## Release Notes

### Notas de la Versión 1.0.0

**¿Qué es nuevo?**

FastAPI RealWorld ha sido adaptado como SUT (Sistema Bajo Prueba) para el proyecto de QA Doctorado 2026. 

**¿Qué necesito hacer?**

1. Ejecuta: `./setup/run_sut.sh`
2. Verifica: `./setup/healthcheck_sut.sh`
3. Comienza a testear: `poetry run pytest`

**¿Hay cambios breaking?**

No. Esto es la primera versión como SUT. El código base de FastAPI RealWorld se mantiene igual.

**¿Cómo reporto bugs?**

Abre un GitHub Issue con:
- Descripción del problema
- Pasos para reproducir
- Output de `./setup/healthcheck_sut.sh --verbose`
- Versión: 1.0.0

---

## Estadísticas de Cambios

### Versión 1.0.0

| Métrica | Valor |
|---------|-------|
| Tests Totales | 90 |
| Tests Pasando | 90+ |
| Cobertura | 85%+ |
| Archivos Nuevos | 7 |
| Archivos Modificados | 2 |
| Líneas de Documentación | 1000+ |
| Tiempo Setup | <5 min |

---

## Roadmap

### Q1 2026
- [x] Seleccionar SUT
- [x] Documentación base
- [x] Scripts de automation
- [ ] CI/CD pipeline

### Q2 2026
- [ ] Extensión de test cases
- [ ] Análisis de cobertura
- [ ] Documentación de hallazgos

### Q3 2026
- [ ] Paper final
- [ ] Presentación
- [ ] Archivado

---

## Referencias

- [Keep a Changelog](https://keepachangelog.com/)
- [Semantic Versioning](https://semver.org/)
- [GitHub Changelog](https://github.blog/changelog/)

---

**Última actualización**: 2026-01-18  
**Mantenedor**: Equipo QA Doctorado 2026
