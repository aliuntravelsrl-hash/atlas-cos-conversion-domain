# CHECKPOINT-CONVERSION-DOMAIN-003

## CONVERSION RUNTIME · HERMES GATEWAY & N8N CHATWOOT CABLEADO

**Fecha:** 09 Sep 2026 · 08:15 (Local Time)
**Modo:** OPERATIONAL SYNCHRONIZATION / EVIDENCE-VERIFIED
**Participantes:** HERMES COMMERCIAL · ATLAS SALES · ATLAS-CABLEADOS (n8n) · DIRECTOR / CCAMEL 360

---

## 1. Hito de Sincronización

Se materializó la conexión física en caliente entre el runtime comercial (Hermes Commercial, VPS2) y el canal de mensajería omnicanal (Chatwoot/WhatsApp vía n8n, VPS1).

```text
CLIENTE (WhatsApp / Chatwoot)
       │
       ↓ (Webhook inbound)
WF-CHATWOOT-HERMES-v1 (n8n)
       │
       ├─→ RPC canal_recibir_mensaje (Supabase CRM)
       │
       ↓ (POST HTTPS /chat)
HERMES COMMERCIAL GATEWAY (:8645 FastAPI / Traefik)
       │
       ↓ (Inferencia LLM OpenRouter / NVIDIA Nemotron)
RESPUESTA ESTRATÉGICA COMERCIAL (Hoteles / Tarifas / Calificación)
       │
       ↓ (POST /conversations/{id}/messages)
CLIENTE (Chatwoot / WhatsApp)
```

---

## 2. Componentes Sincronizados

| Componente | Repositorio / Host | Enlace Físico | Estado |
|---|---|---|---|
| **Hermes Gateway** | `hermes-commercial` (VPS2) | Puerto `8645` expuesto en `https://hermes.srv1587803.hstgr.cloud/chat` | ✅ LIVE |
| **Hermes Dashboard** | `hermes-commercial` (VPS2) | Puerto `4860` en `https://hermes.srv1587803.hstgr.cloud/` | ✅ INTACTO |
| **n8n Responder** | `atlas-cableados` (n8n VPS1) | `WF-CHATWOOT-HERMES-v1` (`Z6wqgUmmtvupZ5dV`) | ✅ LIVE |
| **CRM Inbound Log** | Supabase Cloud | `canal_recibir_mensaje` (`p_canal: whatsapp`) | ✅ LIVE |

---

## 3. Estado de la Pelota en el Dominio

La pelota en el dominio **CONVERSION**:

```text
INTENCIÓN (Mensaje Cliente)
       ↓
CALIFICACIÓN (Filtro & RPC Lead Supabase)
       ↓
OFERTA / CONVERSACIÓN (Hermes AI Gateway :8645)
       ↓
NEGOCIACIÓN (Contexto Hoteles Puerto Plata / Samaná / Punta Cana / Romana)
       ↓
COMPROMISO (En camino a Cotización / Reserva)
```

---

## 4. Próxima Continuidad

1. Observar la conversión y tasa de captura de datos (pax, fechas, destino) en `crm_leads` y `atlas_quotes`.
2. Habilitar la llamada a tools de cotización dinámica (`atlas-sales-mcp`) desde Hermes Gateway para entregar PDFs automáticos (DOC-1 / Gotenberg).
