# Design - Semana 4: Diseño Sistemático de Pruebas

Esta carpeta contiene los artefactos de diseño para la Semana 4 del proyecto de Doctorado en QA 2026.

## Contenido

### 1. oracle_rules.md
**Propósito:** Define las reglas de oráculo para validar el comportamiento del endpoint seleccionado.

**Contenido:**
- 7 oráculos formales (OR-01 a OR-07)
- Criterios PASS/FAIL objetivos
- Cobertura: HTTP codes, JSON structure, performance, data consistency

**Oráculos definidos:**
- **OR-01:** Código HTTP válido
- **OR-02:** Estructura JSON correcta
- **OR-03:** Slug existente → HTTP 200
- **OR-04:** Slug no existente → HTTP 404
- **OR-05:** Slug inválido → HTTP 422
- **OR-06:** Tiempo de respuesta < 1000ms
- **OR-07:** Consistencia de datos

### 2. test_cases.md
**Propósito:** Diseño sistemático de casos de prueba usando Equivalence Partitioning + Boundary Value Analysis.

**Contenido:**
- 12 casos de prueba (TC-01 a TC-12)
- Clases de equivalencia (CE-01 a CE-12)
- Valores límite: longitud 0, 1, 255 caracteres
- Oráculos aplicables por caso
- Comportamiento esperado

**Cobertura:**
- 100% de clases de equivalencia
- 100% de valores límite
- Todos los oráculos aplicados al menos una vez

## Endpoint Seleccionado

**Endpoint:** `GET /api/articles/{slug}`

**Justificación:**
1. Criticidad funcional (core de consulta de artículos)
2. Superficie de entrada amplia (formatos diversos de slug)
3. Valores límite claros (longitud, caracteres especiales)
4. Comportamiento diferenciado (200, 404, 422)
5. Sin autenticación (simplifica ejecución)

## Técnica Aplicada

**Equivalence Partitioning (EP):**
- Divide el dominio de entrada en clases de equivalencia
- Reduce casos de prueba sin sacrificar cobertura
- Identifica valores representativos por clase

**Boundary Value Analysis (BVA):**
- Enfoca en valores límite de cada clase
- Detecta errores en condiciones de borde
- Complementa EP con casos críticos

## Ejecución

**Script:** `scripts/systematic_cases.sh`

**Comando:**
```bash
make systematic-test
```

**Evidencia:**
- `evidence/week4/RUNLOG.md`: Log de ejecución con validación de oráculos
- `evidence/week4/TC-XX.json`: Evidencia JSON por cada caso

**Reporte:**
```bash
make week4-report
```

## Métricas

- **Casos totales:** 12
- **Oráculos formales:** 7
- **Clases de equivalencia:** 12 (100% cobertura)
- **Valores límite:** 4 (100% cobertura)
- **Success rate:** 50% (6 PASS, 6 FAIL)

## Referencias

- **Reporte metodológico:** [reports/week4_report.md](../reports/week4_report.md)
- **Memo semanal:** [memos/week4_memo.md](../memos/week4_memo.md)
- **Evidencia:** [evidence/week4/](../evidence/week4/)

---

**Autor:** Ocean Jungle  
**Fecha:** 4 de febrero de 2026  
**Proyecto:** FastAPI RealWorld Example App - QA Testing Framework
