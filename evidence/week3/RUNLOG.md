# RUNLOG - Evidencia Semana 3

## 2026-01-28 20:00

### Test 1: Disponibilidad (R1) - Escenario Q1
**Comando ejecutado:**
curl -w "@curl-format.txt" -o /dev/null -s http://localhost:8000/api/articles > evidence/week3/api_down.log

**Oráculo aplicado:** HTTP 200 en <1s
**Resultado esperado:** PASS si responde 200 y tiempo <1s

---

### Test 2: Robustez (R2) - Escenario Q2
**Comando ejecutado:**
curl -X POST http://localhost:8000/api/articles -H "Content-Type: application/json" -d '{"title":123}' -i > evidence/week3/robustness.log

**Oráculo aplicado:** Error controlado (4xx/5xx) sin caída del servicio
**Resultado esperado:** PASS si responde error controlado

---

### Test 3: Latencia (R3) - Escenario Q3
**Comando ejecutado:**
ab -n 100 -c 10 http://localhost:8000/api/articles > evidence/week3/latency.log

**Oráculo aplicado:** p95 < 1s
**Resultado esperado:** PASS si p95 < 1s
