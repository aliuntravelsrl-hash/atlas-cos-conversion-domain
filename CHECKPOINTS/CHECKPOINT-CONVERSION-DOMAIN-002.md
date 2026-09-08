# CHECKPOINT-CONVERSION-DOMAIN-002

## CONVERSION → COMPROMISO — Joint Drill

**Fecha:** 08 Sep 2026
**Modo:** READ-ONLY / EVIDENCE-BOUND / DELTA CAPTURE
**Participantes:** ATLAS SALES · HERMES COMMERCIAL · ATLAS SALES MCP · DIRECTOR / CCAMEL 360

## 1. Pregunta del Drill

¿Qué debe ocurrir para que una intención comercial se transforme en compromiso?

```text
INTENCIÓN
 ↓
CALIFICACIÓN
 ↓
OFERTA
 ↓
NEGOCIACIÓN
 ↓
COMPROMISO
```

## 2. Pelota esperada

El Commercial Runtime debe recibir suficiente contexto para decidir y negociar:

```text
CUSTOMER
+ PRODUCT
+ DATES
+ PAX
+ OFFER
+ PRICE
+ MARGIN
+ CONDITIONS
+ STATE
+ POLICY
+ INTENTION
```

ATLAS SALES aporta estructura/mecanismos comerciales; HERMES COMMERCIAL ejecuta la interacción; ATLAS SALES MCP proporciona tooling; CCAMEL 360 observa/reconcilia.

## 3. AS-IS físico encontrado

Supabase contiene representación física para varios puntos del trayecto:

- `crm_leads`: 2,023 registros.
- `crm_activities`: 31,233 registros.
- `crm_events`: 126 registros.
- `crm_event_log`: 15 registros.
- `atlas_quotes`: 36 registros.
- `atlas_offers`: 1 registro.
- `marketing_offers`: 53 registros.
- `offer_date_ranges`: 54 registros.
- `bookings`: 167 registros.
- `atlas_payments`: 30 registros.

También existe contexto de producto reutilizable: `hotels_master`, `hotel_profiles`, `hotel_knowledge`, `rates`, `pricing_engine`, `competitive_intel`.

## 4. Comportamiento esperado vs AS-IS

### Customer Intelligence

**Esperado:** intención + contexto del cliente acompañan la pelota.

**AS-IS:** existe `crm_leads`, con etapas, score, segmento, fuente, fechas, pax, presupuesto, pérdida, preferencias de pago y timestamps; existe un volumen importante de `crm_activities` y `crm_events`.

**Resultado:** REPRESENTADO.

### Product Intelligence

**Esperado:** producto, oferta, precio, condiciones y conocimiento relevante acompañan la decisión.

**AS-IS:** existen `hotels_master`, `hotel_profiles`, `hotel_knowledge`, `rates`, `pricing_engine`, `marketing_offers`, `atlas_offers` y `offer_date_ranges`.

**Resultado:** REPRESENTADO.

### State Intelligence

**Esperado:** estado comercial actual y transición forman parte de la pelota.

**AS-IS:** `crm_leads.stage`, `crm_events`, `crm_event_log`, estados de `marketing_offers`, `atlas_offers` y `bookings` materializan diferentes estados.

**Resultado:** REPRESENTADO PARCIALMENTE como una continuidad transversal única.

### Offer / Negotiation

**Esperado:** la oferta debe materializar la decisión comercial y la negociación debe dejar estado/evidencia antes del compromiso.

**AS-IS:** `atlas_offers` posee campos de descuento negociado, `negotiated_by`, `negotiated_at`, margen y estado; sin embargo, el snapshot actual tiene 1 `atlas_offer` y `negotiated_at` no está poblado en ese registro.

**Resultado:** MECANISMO REPRESENTADO; EVIDENCIA ACTUAL DE NEGOCIACIÓN NO DEMOSTRADA EN EL SNAPSHOT.

### Commitment

**Esperado:** el resultado de la negociación debe producir un compromiso identificable que pueda continuar hacia obligación económica.

**AS-IS:** `bookings` materializa conversiones/ventas confirmadas y contiene snapshots de oferta/condiciones, pero la causalidad universal `negociación → compromiso` no está demostrada para todo el universo.

**Resultado:** REPRESENTADO; CONTINUIDAD CAUSAL UNIVERSAL NO DEMOSTRADA.

## 5. DELTAS capturados

### DELTA-D9 — State Intelligence transversal

Existen múltiples representaciones de estado (`crm_leads`, `crm_events`, `crm_event_log`, `marketing_offers`, `atlas_offers`, `bookings`), pero no queda demostrada una única pelota de estado comercial que atraviese todos los componentes.

### DELTA-D10 — Negotiation evidence

El mecanismo de negociación existe en `atlas_offers`, pero el snapshot actual no demuestra una negociación materializada (`negotiated_at` no poblado en el registro existente).

### DELTA-D11 — Conversion causal continuity

La existencia de leads, quotes, offers y bookings demuestra representación de etapas, pero no demuestra universalmente que cada booking provenga causalmente de la cadena intención → calificación → oferta → negociación → compromiso.

### DELTA-D12 — Measurement at conversion

`offer_interactions` y `offer_metrics` existen como mecanismos, pero ambos tienen actualmente 0 registros. Por tanto, la medición estructurada de interacción/oferta no está demostrada como cadena operativa actual.

## 6. No se resuelve

Los DELTAS anteriores no se convierten en GAP/EVO durante este Drill. No se modifica ningún componente.

## 7. Aprendizaje del Drill

La estructura confirma una separación útil:

```text
CUSTOMER INTELLIGENCE
        +
PRODUCT INTELLIGENCE
        +
STATE INTELLIGENCE
        +
POLICY
        ↓
COMMERCIAL RUNTIME
        ↓
DECISIÓN / NEGOCIACIÓN
        ↓
COMPROMISO
```

El dominio CONVERSION debe estudiar principalmente la **continuidad del contexto**, no solamente la existencia de agentes o tablas.

## 8. Posición de la pelota

La pelota permanece en:

```text
CONVERSIÓN → COMPROMISO
```

El siguiente Drill debe comprobar cómo el compromiso se transforma en **OBLIGACIÓN ECONÓMICA → PAGO**, manteniendo las mismas cuatro perspectivas sincronizadas.

## 9. Genealogía

Este checkpoint nace de `CHECKPOINT-CONVERSION-DOMAIN-001` y `CEND-CONVERSION-JOINT-001`. No reemplaza ninguno de ellos; constituye el siguiente estado verificable del organismo.
