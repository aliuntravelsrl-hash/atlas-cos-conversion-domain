# Synchronization Map
**Última actualización:** 09 Sep 2026 · ATLAS-TECH

## Current synchronized lane

```text
DIRECTOR / CCAMEL 360
        │
        ↓
   ┌───────────────┐
   │ CONVERSION    │
   │    CONTEXT    │
   └───────────────┘
        │
   ┌────┴──────────────┐
   ↓                   ↓
ATLAS SALES      HERMES COMMERCIAL (:8645 Gateway LIVE)
   │                   │
   └─────── SYNC ──────┘
           │
   ┌───────┴───────────────┐
   ↓                       ↓
WF-CHATWOOT-HERMES-v1   SALES MCP
(n8n Inbound LIVE)         │
   │                       ↓
   └─────────────────→ NEXT RESULT (COMPROMISO / BOOKING)
```

## Componentes Activos Sincronizados

1. **Hermes Commercial Gateway HTTP:** `https://hermes.srv1587803.hstgr.cloud/chat` (FastAPI en puerto 8645).
2. **Chatwoot / WhatsApp Dispatcher:** `WF-CHATWOOT-HERMES-v1` (`Z6wqgUmmtvupZ5dV`).
3. **CRM Ingestion & Memory:** Supabase RPC `canal_recibir_mensaje` y `logs_operativos`.

## Evidence references
- `EVIDENCE/EVIDENCE-CONVERSION-001-HERMES-GATEWAY-N8N.md`
- `CHECKPOINTS/CHECKPOINT-CONVERSION-DOMAIN-003.md`
