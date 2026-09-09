# EVIDENCE-CONVERSION-006: SUPPLIER INGESTION & SRM FOLLOWUP PIPELINE

**Fecha de Ejecución:** 09 de Septiembre de 2026 · 09:06 (Local Time)  
**Dominio:** COS Conversión / SRM Supplier Governance / Pipeline Operativo  
**Actores:** Antigravity (ATLAS-TECH) · Director General Aldo Hilario · n8n WF-SUPPLIER-FOLLOWUP-v1 · Supabase Cloud · Telegram Bot  
**Estado:** ✅ CERTIFICADO E2E Y SELLADO EN GIT

---

## 1. Contexto y Antecedentes en Commits

1. **Contrato de Ingesta Asíncrona (EVO v2):**
   - **Commit `1f013ae` (`atlas-curator-office`):** `contract(curator): formalizar EVO Supplier Ingestion Technical Execution Contract v2`.
   - Define la cadena canónica de estructuración de oferta y bloqueos:
     $$\text{RAW\_SUPPLIER\_EVIDENCE} \rightarrow \text{INGESTION\_ATTEMPT} \rightarrow \text{PARSED\_CANDIDATE} \rightarrow \text{IDENTITY\_RESOLUTION} \rightarrow \text{VALIDATION} \rightarrow \text{CORE 2 (\texttt{atlas\_block\_inventory})}$$

2. **Protocolo de Negociación y Ciclo de Vida (ONP-v1):**
   - **Commit `42b6608` (`aliun-rrhh-v2`):** `protocol(ONP-v1): Offer Negotiation Protocol`.
   - Define el ciclo de vida de 11 estados incluyendo `awaiting_supplier` para solicitudes que requieren negociación o cotización externa con mayoristas (Travellanda, RateHawk, Yanolja, TBO, VDT).

3. **Pipeline de Seguimiento Automatizado:**
   - **Commit `fe5fcc7` (`atlas-cableados`):** `feat(crm): WF-SUPPLIER-FOLLOWUP-v1 — CRM seguimiento proveedores`.
   - Workflow n8n con cron de 2 horas sobre `public.supplier_requests`.

---

## 2. Ejecución del Test E2E de Simulación

Se ejecutó la simulación controlada del ciclo completo:
- Ingesta de Solicitud en `public.supplier_requests`
- Evaluación de SLAs y límites de tiempo por tipo de requerimiento
- Despacho de alerta con semáforo y enlace al proveedor hacia Telegram del Director
- Actualización de estado en base de datos y log en `public.logs_operativos`

### Traza de Ejecución:
```text
--- INICIO TEST E2E: INGESTA PROVEEDOR & PIPELINE DE SEGUIMIENTO ---

[1/4] Creando solicitud en public.supplier_requests...
Supplier Request creado: 201 [
  {
    id: 2,
    referencia: 'REQ-SUPP-208680',
    tipo: 'confirmation',
    proveedor: 'travellanda',
    message_id: 'MSG:98765432',
    booking_ref: 'BK-TEST-2026-X9',
    descripcion: 'Solicitud asíncrona de confirmación de tarifa y bloqueo para Serenade All Suites.',
    estado: 'enviado',
    fecha_envio: '2026-09-09T08:06:48.681+00:00',
    fecha_acuse: '2026-09-09T08:06:48.687+00:00',
    fecha_resolucion: null,
    fecha_followup: '2026-09-09T13:06:48.68+00:00',
    created_at: '2026-09-09T13:06:47.103101+00:00',
    updated_at: '2026-09-09T13:06:47.103101+00:00'
  }
]

[2/4] Ejecutando clasificación y SLA tracking...
Evaluación: 5h transcurridas (Límite: 4h) -> Escalar: true | Estado: escalado

[3/4] Enviando alerta de seguimiento a Telegram del Director...
Telegram notificado: ✅ ENVIADO CON ÉXITO (Msg ID: 6685)

[4/4] Actualizando public.supplier_requests y registrando en public.logs_operativos...
Update Status: 200
Log Operativo Status: 201

--- TEST E2E COMPLETADO EXITOSAMENTE ---
```

---

## 3. Matriz de SLAs Auditada

| Tipo de Solicitud | Límite SLA | Acción al Vencer | Destino de Alerta |
|---|---|---|---|
| `confirmation` | 4 Horas | Escalado a `🔴 ESCALADO` | Telegram Director + `logs_operativos` |
| `cancellation` | 24 Horas | Escalado a `🔴 ESCALADO` | Telegram Director + `logs_operativos` |
| `amendment` | 48 Horas | Escalado a `🔴 ESCALADO` | Telegram Director + `logs_operativos` |
| `complaint` | 72 Horas | Escalado a `🔴 ESCALADO` | Telegram Director + `logs_operativos` |

---

## 4. Invariante y Cierre

El dominio de conversión cuenta ahora con:
1. **Atención Síncrona Inmediata:** Hermes Commercial Gateway (`:8645`) + Tool Calling canónico contra Supabase (Core 1 / Core 2).
2. **Atención Asíncrona Externa:** `supplier_requests` + `WF-SUPPLIER-FOLLOWUP-v1` + Notificaciones Telegram al Director + Ingesta estructurada EVO v2 hacia `atlas_block_inventory`.
