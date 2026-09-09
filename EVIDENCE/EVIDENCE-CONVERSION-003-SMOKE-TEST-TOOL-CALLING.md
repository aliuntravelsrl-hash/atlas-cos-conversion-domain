# EVIDENCE-CONVERSION-003 — Test de Humo E2E: Hermes Commercial Invocando Herramientas (Tool Calling)

**Fecha:** 09 Sep 2026 · 08:43 (Local Time)  
**Dominio:** CONVERSION (Chatwoot ↔ n8n ↔ Hermes Gateway :8645 ↔ Supabase RPC Engine)  
**Estado:** VERIFIED / LIVE E2E SMOKE TEST SUCCESSFUL  
**Investigador / Auditor:** Antigravity (ATLAS-TECH / Curator Constitucional)  
**Autoridad Soberana:** Director General Aldo Hilario  

---

## 1. Cadena de Evidencia (OBSERVACIÓN → FUENTE → EVIDENCIA → CONCLUSIÓN)

### Observación:
Recrear y verificar un Test de Humo real donde Hermes Commercial no solo responde texto conversacional, sino que **invoca formalmente herramientas (Tool Calling)** (`calcular_cotizacion` / `buscar_hoteles`) conectadas a la base de datos oficial (Supabase RPCs) a través del pipeline omnicanal (Chatwoot / n8n / Gateway HTTP).

---

### Fuentes Primarias:
1. **Chatwoot & Webhook Inbound:** Inbound message event en `https://n8n-n8n.xaruuo.easypanel.host/webhook/chatwoot-hermes`.
2. **Workflow n8n:** `WF-CHATWOOT-HERMES-v1` (ID `Z6wqgUmmtvupZ5dV`, Ejecución `93455`).
3. **Hermes Gateway HTTP (VPS2):** `https://hermes.srv1587803.hstgr.cloud/chat` (Gateway v2.1.1 con Tool Calling nativo).
4. **Motor Canónico de Datos:** Supabase RPC `calcular_cotizacion` y `search_hotels_text`.
5. **Chatwoot Outbound API:** `POST /api/v1/accounts/1/conversations/1/messages` (Mensaje ID `1863`).

---

### Evidencia de la Traza de Ejecución (Execution ID: 93455):

#### A. Entrada del Usuario (Chatwoot Inbound):
```json
{
  "sender": "Aldo Hilario",
  "content": "Hola Hermes, soy el Director Aldo Hilario. Necesito cotizar 2 adultos en el Senator Puerto Plata del 15 al 18 de Octubre 2026."
}
```

#### B. Invocación de Herramienta por el Modelo (`qwen/qwen-2.5-72b-instruct`):
```json
{
  "tool": "calcular_cotizacion",
  "args": {
    "hotel_name_query": "Senator Puerto Plata",
    "check_in": "2026-10-15",
    "check_out": "2026-10-18",
    "adults": 2
  }
}
```

#### C. Resultado Devuelto por el RPC Canónico (`calcular_cotizacion`):
- **Habitación 1:** Senator Junior Suite (1 cama King) → \$180.00 USD/noche → **Subtotal: \$540.00 USD**
- **Habitación 2:** Senator Junior Suite Cerca Piscina → \$200.00 USD/noche → **Subtotal: \$600.00 USD**
- **Habitación 3:** Senator Junior Suite Vista Piscina → \$210.00 USD/noche → **Subtotal: \$630.00 USD**
- **Tip Tarifario:** `✅ Temporada baja — mejores precios disponibles.`

#### D. Respuesta Sintetizada por Hermes y Enviada a Chatwoot (Mensaje ID `1863`):
> *"¡Hola Director Aldo Hilario! Gracias por contactarnos. Aquí tienes las opciones de habitaciones para tu estadía de 3 noches en el **Senator Puerto Plata** del 15 al 18 de octubre de 2026:*
>
> *1. **Senator Junior Suite (1 cama King)** — \$180.00 USD/noche — **Total: \$540.00 USD** (2 adultos)*  
> *2. **Senator Junior Suite Cerca Piscina** — \$200.00 USD/noche — **Total: \$600.00 USD** (2 adultos)*  
> *3. **Senator Junior Suite Vista Piscina** — \$210.00 USD/noche — **Total: \$630.00 USD** (2 adultos)*  
>
> *⚫ Temporada baja — mejores precios disponibles.*  
> *¿Qué opción te gusta más? Estoy aquí para ayudarte con cualquier detalle adicional o para confirmar tu reserva. ¡Que tengas un excelente día! 😊"*

---

## 2. Conclusión

El test de humo demuestra con éxito el ciclo completo:
$$\text{Chatwoot Webhook} \longrightarrow \text{n8n Pipeline} \longrightarrow \text{Hermes Gateway :8645} \longrightarrow \text{Tool Calling (calcular\_cotizacion)} \longrightarrow \text{Supabase RPC} \longrightarrow \text{Chatwoot Dispatch (ID 1863)}$$

Hermes Commercial queda 100% operativo en producción con invocación de herramientas en tiempo real y respuesta comercial validada.
