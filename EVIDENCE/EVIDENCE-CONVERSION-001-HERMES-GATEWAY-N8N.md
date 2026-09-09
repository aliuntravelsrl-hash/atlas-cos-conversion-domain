# EVIDENCE-CONVERSION-001 — Hermes Commercial Gateway HTTP & n8n Live Wire
**Fecha:** 09 Sep 2026 · 08:12 (Local Time)
**Dominio:** CONVERSION (Inbound / Calificación / Negociación Runtime)
**Estado:** VERIFIED / LIVE IN PRODUCTION

---

## 1. Cadena de Evidencia (OBSERVACIÓN → FUENTE → EVIDENCIA → CONCLUSIÓN)

### Observación:
Hermes Commercial requiere un runtime HTTP real capaz de recibir eventos inbound de Chatwoot/WhatsApp, procesar contexto de viajes con IA y despachar respuestas operativas en tiempo real.

### Fuentes:
1. **VPS2 Container:** `hermes-agent-dpkf-hermes-agent-1` en `srv1587803.hstgr.cloud` (puerto 8645).
2. **Traefik Reverse Proxy:** Labels en `/docker/hermes-agent-dpkf/docker-compose.yml` con router `hermes-commercial-gateway`.
3. **Workflow n8n:** `WF-CHATWOOT-HERMES-v1` (ID: `Z6wqgUmmtvupZ5dV`).
4. **Supabase Database:** RPC `canal_recibir_mensaje` y tabla `logs_operativos`.

### Evidencia:
1. **Traefik Health Check:**
   - URL: `https://hermes.srv1587803.hstgr.cloud/health`
   - Response: `{"status":"ok","gateway":"hermes-commercial","port":8645,"version":"2.0.0"}` (HTTP 200 OK).
2. **Dashboard 4860 Preservado:**
   - URL: `https://hermes.srv1587803.hstgr.cloud/`
   - Response: HTTP 302 hacia `/login` (intacto).
3. **Inferencia LLM en Tiempo Real:**
   - Endpoint: `POST https://hermes.srv1587803.hstgr.cloud/chat`
   - Model: `nvidia/nemotron-3-super-120b-a12b:free` con fallback a `nex-agi/nex-n2.5-pro:free`.
4. **n8n E2E Inbound Execution (Execution ID: 93409):**
   - Webhook Inbound Chatwoot `chatwoot-hermes` → `02_FILTRAR` → `03_APLICA` → `03B_REGISTRAR_SESION` → `04_HERMES_RESPONDER` → `04B_FORMAT_HERMES_MSG` → `05_RESPONDER_CW` → `06_ACK`.
   - Estado: `SUCCESS`.

### Conclusión:
La capa de ejecución comercial (Hermes Commercial) queda físicamente conectada con n8n y Chatwoot/WhatsApp, cerrando la brecha de respuestas estáticas y habilitando la negociación dinámica de conversión.
