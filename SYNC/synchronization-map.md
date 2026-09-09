# Synchronization Map
**Última actualización:** 09 Sep 2026 · ATLAS-TECH (Verificado E2E)

## Current synchronized lane

```text
DIRECTOR / CCAMEL 360 / CONSTITUTIONAL GOVERNANCE
        │
        ↓
   ┌───────────────┐
   │ CONVERSION    │
   │    CONTEXT    │
   └───────────────┘
        │
   ┌────┴─────────────────────────────┐
   ↓                                  ↓
ATLAS SALES                     HERMES COMMERCIAL (:8645 Gateway LIVE)
   │                                  │
   └──────────────── SYNC ────────────┘
                     │
   ┌─────────────────┼─────────────────┐
   ↓                 ↓                 ↓
WF-CHATWOOT-HERMES   SALES MCP / RPC  WF-SUPPLIER-FOLLOWUP
(n8n Inbound LIVE)   (Supabase Cloud) (SRM Async & SLA LIVE)
   │                 │                 │
   └─────────────────┼─────────────────┘
                     ↓
          COMPROMISO & NEGOCIACIÓN
                     ↓
        ABONO FINANCIERO (atlas_payments)
                     ↓
           FACTURA & VOUCHER PDF
                     ↓
       CCAMEL 360 & OPERATIONAL LOGS
```

## Componentes Activos Sincronizados

1. **Hermes Commercial Gateway HTTP:** `https://hermes.srv1587803.hstgr.cloud/chat` (FastAPI v2.3.0 en puerto 8645, soporte nativo Function Calling).
2. **Chatwoot / WhatsApp Dispatcher:** `WF-CHATWOOT-HERMES-v1` (`Z6wqgUmmtvupZ5dV` en n8n).
3. **CRM Pipeline & Stage Management:** `public.crm_leads` (etapas: nuevo, contactado, cotizado, negociacion, cerrado_ganado, cerrado_perdido).
4. **Financial Engine & Voucher Dispatch:** `public.atlas_payments`, `public.bookings`, `generar-voucher-pdf` y alertas a Telegram.
5. **SRM Supplier Ingestion & Followup:** `public.supplier_requests`, `WF-SUPPLIER-FOLLOWUP-v1` (Cron cada 2h con SLAs 4h/24h/48h/72h), `raw_supplier_evidence` e `ingestion_attempts` (EVO v2).

## Evidence references
- `EVIDENCE/EVIDENCE-CONVERSION-001-HERMES-GATEWAY-N8N.md`
- `EVIDENCE/EVIDENCE-CONVERSION-002-FRONT-G-RUNTIME-TRACE.md`
- `EVIDENCE/EVIDENCE-CONVERSION-003-SMOKE-TEST-TOOL-CALLING.md`
- `EVIDENCE/EVIDENCE-CONVERSION-004-CRM-PIPELINE-TOOL-CALLING.md`
- `EVIDENCE/EVIDENCE-CONVERSION-005-SRM-FINANCIAL-VOUCHER-TOOL-CALLING.md`
- `EVIDENCE/EVIDENCE-CONVERSION-006-SUPPLIER-INGESTION-FOLLOWUP-PIPELINE.md`
- `CHECKPOINTS/CHECKPOINT-CONVERSION-DOMAIN-001.md`
- `CHECKPOINTS/CHECKPOINT-CONVERSION-DOMAIN-002.md`
- `CHECKPOINTS/CHECKPOINT-CONVERSION-DOMAIN-003.md`
- `CHECKPOINTS/CHECKPOINT-CONVERSION-DOMAIN-004.md`
- `CHECKPOINTS/CHECKPOINT-CONVERSION-DOMAIN-005.md`
