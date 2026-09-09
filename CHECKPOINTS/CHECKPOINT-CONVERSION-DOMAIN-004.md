# CHECKPOINT-CONVERSION-DOMAIN-004

## CONVERSION RUNTIME · FRONT G DELIMITACIÓN & TRAZA DE RUNTIME HERMES

**Fecha:** 09 Sep 2026 · 08:32 (Local Time)  
**Modo:** EPISTEMIC AUDIT & RUNTIME RECONSTRUCTION / EVIDENCE-VERIFIED  
**Participantes:** HERMES COMMERCIAL · ATLAS SALES · CCAMEL 360 · DIRECTOR / ANTIGRAVITY  

---

## 1. Hito Epistémico (FRONT G Resuelto)

Se completó el escaneo forense de los **3,425 archivos de sesión históricos** (`/opt/data/sessions/*.json`) y de los **73,897 mensajes** en la base de datos principal (`/opt/data/state.db`, 4.1 GB) del contenedor de Hermes Commercial en VPS2 (`hermes-agent-dpkf-hermes-agent-1`).

```text
CONTRATO SOUL v2 (Prompt / Intención)
       │ "Mis herramientas: atlas-sales-mcp (14 tools)"
       │
       ├─→ FRONT G AS-IS: Sin cliente MCP activo en runtime histórico
       │   (0 tool_calls materializados en 3,425 sesiones)
       │
       ↓ (Generación Conversacional Contextual / Precios Indicativos)
RESPUESTA TEXTUAL AL CLIENTE
```

---

## 2. Hallazgos Auditados

1. **Frontera de Ejecución de Herramientas:**
   - Palabras clave como `calcular_cotizacion`, `buscar_hoteles` y `atlas-sales-mcp` existían en 32 archivos de sesión (dumps de contexto e historial de prompts) y en consultas de auditoría en `state.db`.
   - **Total de Invocaciones MCP Estructuradas (`tool_calls`): 0**.
   - En el runtime histórico de Hermes, el agente operaba con herramientas de mensajería, respondiendo textualmente sin socket de terminal/MCP activo hacia el motor canónico de cotización.

2. **Evidencia Primaria Generada:**
   - Registrada en [`EVIDENCE/EVIDENCE-CONVERSION-002-FRONT-G-RUNTIME-TRACE.md`](../EVIDENCE/EVIDENCE-CONVERSION-002-FRONT-G-RUNTIME-TRACE.md).

3. **Arquitectura TO-BE Habilitada con el Gateway HTTP (:8645):**
   - Con la entrada en producción de `hermes-commercial` Gateway HTTP (FastAPI) y su cableado a `WF-CHATWOOT-HERMES-v1`, la llamada canónica a Supabase / MCP queda desacoplada de forma determinista y orquestable directamente desde los nodos de n8n y endpoints REST.

---

## 3. Estado de FRONT G en el Mapa de Conversión

| Componente | AS-IS Histórico | TO-BE Actual (Live) |
|---|---|---|
| **Ruteo de Intención** | Textual / Prompt | n8n Classifier + Hermes Gateway HTTP |
| **Generación de Oferta** | Completado LLM directo | Inferencia LLM Nemotron/Nex + Reglas Comerciales |
| **Cálculo Canónico** | No invocado (0 tool calls) | Enlace canónico vía n8n / Supabase RPC |
