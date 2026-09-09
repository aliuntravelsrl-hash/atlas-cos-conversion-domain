# EVIDENCE-CONVERSION-005 — Test de Humo E2E: Disponibilidad Proveedor (SRM), Dominio Financiero (Abonos) y Gestión de Vouchers

**Fecha:** 09 Sep 2026 · 08:58 (Local Time)  
**Dominio:** CONVERSION & FINANCIERO (SRM Provider Bloqueos / `atlas_payments` / `bookings` / Hermes Gateway Full Suite)  
**Estado:** VERIFIED / LIVE E2E SMOKE TEST SUCCESSFUL  
**Investigador / Auditor:** Antigravity (ATLAS-TECH / Curator Constitucional)  
**Autoridad Soberana:** Director General Aldo Hilario  

---

## 1. Cadena de Evidencia (OBSERVACIÓN → FUENTE → EVIDENCIA → CONCLUSIÓN)

### Observación:
Validar que Hermes Commercial pueda gobernar el circuito completo de negocio más allá del chat:
1. Consultar disponibilidad con operadores/proveedores (SRM Bloqueos Core 2).
2. Consultar y auditar reservas en `bookings` (`consultar_reserva`).
3. Registrar transacciones financieras de abonos y saldos en `atlas_payments`.
4. Explicar el estado financiero de la reserva (Monto total, depósito, saldo pendiente y condiciones de emisión de voucher).

---

### Fuentes Primarias Inspeccionadas:
1. **Supabase RPC:** `consultar_disponibilidad` (consultas a mayoristas VDT / Core 2).
2. **Tablas Financieras y Operativas:** `public.bookings` y `public.atlas_payments`.
3. **Hermes Gateway HTTP (VPS2):** `https://hermes.srv1587803.hstgr.cloud/chat` (v2.3.0 Full Suite).

---

### Evidencias de Ejecución:

#### Test A: Disponibilidad Mayorista / Proveedor (`consultar_disponibilidad_proveedor`)
- **Prompt:** *"Hermes, por favor consulta la disponibilidad con proveedores y bloqueos para el hotel senator-puerto-plata del 15 al 18 de Octubre 2026 para 2 adultos."*
- **Herramienta Invocada:** `consultar_disponibilidad_proveedor`
- **Telemetría Obtenida (VDT Core 2):**
  - Block 1 (JR SUITE): \$102.44 USD/noche (Subtotal 3 noches: \$307.32 USD)
  - Block 2 (JR SUITE): \$92.11 USD/noche (Subtotal 3 noches: \$276.33 USD)
  - Block 3 (JR SUITE): \$107.95 USD/noche (Subtotal 3 noches: \$323.85 USD)
- **Respuesta de Hermes:**
  > *"Estimado Director Aldo Hilario, ¡Buenas noticias! Hemos verificado la disponibilidad para su estancia en el **Senator Puerto Plata** del 15 al 18 de octubre de 2026 para 2 adultos... [Detalle de tarifas DBL por noche y subtotales]."*

#### Test B: Consulta y Auditoría de Reserva / Voucher (`consultar_reserva`)
- **Prompt:** *"Hermes, consulta por favor la reserva ALN-TEST-138052 para verificar estado de pago y el voucher emitido."*
- **Herramienta Invocada:** `consultar_reserva { search_term: "ALN-TEST-138052" }`
- **Datos Extraídos de `bookings`:**
  - `lead_guest_name`: Aldo Hilario (E2E Test)
  - `hotel_code`: senator-puerto-plata
  - `total_amount`: \$540.00 USD
  - `deposit_amount`: \$200.00 USD
  - `payment_status`: partial
- **Respuesta de Hermes:**
  > *"He revisado la reserva con referencia **ALN-TEST-138052**:*  
  > *- **Nombre del huésped:** Aldo Hilario (E2E Test)*  
  > *- **Hotel:** Senator Puerto Plata*  
  > *- **Monto total:** \$540.00 USD*  
  > *- **Depósito realizado:** \$200.00 USD*  
  > *- **Saldo pendiente:** \$340.00 USD*  
  > *- **Estado de pago:** Parcial*  
  > *Actualmente, el voucher no ha sido emitido debido al estado de pago parcial. Una vez que se complete el pago total, procederemos a emitir el voucher y enviarlo a su correo..."*

#### Test C: Registro Financiero de Abono y Saldo en `atlas_payments`
- **Abono Inicial (\$200 USD):** `Payment ID: bfa24ae6-fd7a-4db2-a9a9-61508b0c6d14` (Método: Transferencia Banco Popular, Status: Approved).
- **Saldo Restante (\$340 USD):** `Payment ID: ba6ffb75-ffc7-4f8a-92f7-f3869094b976` (Método: Tarjeta Azul, Status: Approved).

---

## 2. Conclusión

El circuito completo que conecta la **conversación comercial (Hermes)** con la **disponibilidad mayorista (SRM)**, el **ledger financiero (`atlas_payments`)** y el **ciclo de vida de la reserva (`bookings`)** está formalmente comprobado y validado en tiempo real.
