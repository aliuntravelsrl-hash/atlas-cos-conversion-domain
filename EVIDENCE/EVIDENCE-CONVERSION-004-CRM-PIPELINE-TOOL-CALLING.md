# EVIDENCE-CONVERSION-004 — Test de Humo CRM Pipeline: Hermes Commercial Avanzando y Consultando Oportunidades

**Fecha:** 09 Sep 2026 · 08:50 (Local Time)  
**Dominio:** CONVERSION (CRM Pipeline / Supabase `crm_leads` / Hermes Gateway Tool Calling)  
**Estado:** VERIFIED / LIVE E2E SMOKE TEST SUCCESSFUL  
**Investigador / Auditor:** Antigravity (ATLAS-TECH / Curator Constitucional)  
**Autoridad Soberana:** Director General Aldo Hilario  

---

## 1. Cadena de Evidencia (OBSERVACIÓN → FUENTE → EVIDENCIA → CONCLUSIÓN)

### Observación:
Validar que Hermes Commercial pueda gobernar y avanzar activamente el pipeline de ventas en el CRM nativo (`public.crm_leads`) mediante Tool Calling en tiempo real (consultar métricas del embudo, actualizar etapas a `abono_recibido` o `confirmada`, y registrar timestamps de cobro y voucher).

---

### Fuentes Primarias:
1. **Base de Datos CRM:** Supabase Cloud `public.crm_leads`.
2. **Hermes Commercial Gateway HTTP (VPS2):** `https://hermes.srv1587803.hstgr.cloud/chat` (v2.2.0 con CRM tools).
3. **Herramientas Implementadas y Ejecutadas:**
   - `consultar_pipeline`: Muestreo y consolidación de métricas por etapa.
   - `avanzar_pipeline`: Transición de etapa en `crm_leads` con actualización de timestamps (`abono_recibido_at`, `saldo_cobrado_at`, `voucher_enviado_at`).

---

### Evidencias de Ejecución:

#### Test 1: Consulta Ejecutiva del Pipeline (`consultar_pipeline`)
- **Prompt:** *"Hola Hermes, ¿cuál es el resumen y métricas actuales de nuestro pipeline de ventas en el CRM?"*
- **Invocación:** `tool: consultar_pipeline, args: {}`
- **Telemetría Devuelta:**
  - `confirmada`: 1
  - `deposito_recibido`: 1
  - `perdido`: 1
  - `nuevo`: 47
- **Respuesta de Hermes:**
  > *"Aquí le presento un resumen de las métricas actuales de nuestro pipeline de ventas en el CRM:*  
  > *- Total de Oportunidades: 50*  
  > *- Confirmadas: 1 | Depósito Recibido: 1 | Nuevas: 47"*

#### Test 2: Avance de Etapa en CRM (`avanzar_pipeline`)
- **Prompt:** *"Hermes, el cliente con teléfono 1 849 360 9283 (Moises Heredia) acaba de pagar el saldo completo. Por favor confirma su reserva en el CRM."*
- **Invocación:** `tool: avanzar_pipeline, args: { phone: "1 849 360 9283", new_stage: "confirmada" }`
- **Efecto en Base de Datos Supabase:**
  - Lead ID: `f01701d0-89bc-4459-920a-990ea0c54180` (Moises Heredia)
  - `stage`: `confirmada`
  - `saldo_cobrado_at`: `2026-09-09T12:49:22.825845+00:00`
  - `voucher_enviado_at`: `2026-09-09T12:49:22.825855+00:00`
- **Respuesta de Hermes:**
  > *"¡Excelente noticia, Moises Heredia ha completado su pago! Su reserva en el Occidental Caribe ya está confirmada en nuestro sistema."*

---

## 2. Conclusión

El pipeline CRM queda plenamente integrado al motor de conversación e inferencia de Hermes Commercial. Las transiciones comerciales ahora se reflejan de forma atómica y auditable en la base de datos central de Supabase.
