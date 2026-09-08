# CEND-CONVERSION-JOINT-001

## Joint Cold Entry — Conversion Domain

**Fecha:** 08 Sep 2026
**Modo:** COLD ENTRY / READ-ONLY FIRST / EVIDENCE-BOUND / GOVERNED CONTINUATION
**Dominio:** CONVERSION

## 1. Entrada

La entrada conjunta se realiza sobre la ruta persistida del `atlas-cos-conversion-domain`. No se inicia una búsqueda arqueológica desde cero.

## 2. Fuentes físicas participantes

### ATLAS SALES

El README actual lo identifica como el frente comercial oficial de Aliun Travel, con ventas, arquitectura de cierre, operación B2B/B2C y KPIs. Su estructura documentada incluye routing, rutinas comerciales, tools y knowledge.

### HERMES COMMERCIAL

El README actual lo identifica como **Commercial Runtime / executor**, responsable de ventas omnicanal, CRM, pricing y booking. Declara como dependencias `atlas-sales-mcp`, Supabase y otros mecanismos de ejecución comercial. Declara que implementa, pero no duplica, la doctrina del COS.

### ATLAS SALES MCP

El README actual lo identifica como **infraestructura / MCP Server / herramientas de dominio**, consumidor principal de Hermes Commercial. Su función es exponer herramientas de ventas y booking; no es autoridad ni contenedor de doctrina.

### DIRECTOR / CCAMEL 360

Representación soberana de visión y reconciliación 360 del dominio. Su función en este Drill es observar el dominio completo, sus relaciones, resultados, evidencia y evolución; la autoridad de cambio permanece en el Director.

## 3. Sincronización ontológica

```text
                         CONVERSION
                             │
             ┌───────────────┼───────────────┐
             ↓               ↓               ↓
        ATLAS SALES    HERMES COMMERCIAL   CCAMEL 360
             │               │               │
             │            execution          │
        mechanisms           │          observation /
             │               │          reconciliation
             └───────────────┼───────────────┘
                             ↓
                       ATLAS SALES MCP
                             ↓
                         TOOLS / CALL
                             ↓
                        NEXT RESULT
```

Esta representación no afirma que todos los handoffs estén causalmente demostrados. Define el plano conjunto desde el cual se comprobarán.

## 4. Pelota común

La pelota del dominio es el contexto comercial necesario para producir el siguiente resultado:

```text
CLIENTE
+ INTENCIÓN
+ PRODUCTO
+ FECHAS
+ PAX
+ OFERTA
+ PRECIO
+ MARGEN
+ CONDICIONES
+ NEGOCIACIÓN
+ DECISIÓN
```

El contenido real de cada campo debe ser confirmado por evidencia durante el Drill.

## 5. Cognitive + Learn

El dominio participa en el mismo comportamiento universal:

```text
OBSERVACIÓN
 ↓
EVIDENCIA
 ↓
COMPARABILIDAD
 ↓
RESULTADO
 ↓
OUTCOME SIGNAL
 ↓
LEARNING
 ↓
PATTERN
 ↓
EVO
 ↓
TO-BE
 ↓
GOVERNED BUILD
 ↓
VALIDATION
 ↓
NEW AS-IS
 ↺
```

El Domain Repository conserva la representación navegable y la genealogía; los repositorios participantes conservan sus propias implementaciones.

## 6. Estado epistemológico de entrada

### Confirmado

- Los tres repositorios físicos existen y tienen funciones diferenciadas.
- ATLAS SALES y HERMES COMMERCIAL representan capas distintas del mismo territorio comercial.
- ATLAS SALES MCP es infraestructura de herramientas para la ejecución comercial.
- La Constitución del COS continúa en `atlas-cos-v1`.
- El Domain Repository ya contiene ruta, checkpoints y reglas de Drill.

### No asumido

- No se asume que la cadena completa CONVERSION → COMPROMISO → OBLIGACIÓN → PAGO esté causalmente demostrada de extremo a extremo.
- No se asume que toda capacidad, estrategia o inteligencia necesaria esté correctamente conectada en cada handoff.
- No se convierte documentación declarativa en evidencia de ejecución.

## 7. Próximo movimiento de la pelota

La CEND conjunta queda cerrada en el punto:

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
   ↓
OBLIGACIÓN ECONÓMICA
   ↓
PAGO
```

El siguiente Drill continúa en **CONVERSIÓN → COMPROMISO**, manteniendo ATLAS SALES y HERMES COMMERCIAL en paralelo, ATLAS SALES MCP como infraestructura y DIRECTOR / CCAMEL 360 como perspectiva de reconciliación.

## 8. Delta policy

Todo resultado que no coincida con el comportamiento esperado se registra como **DELTA**. La resolución GAP / EVO queda para la fase posterior gobernada.

## 9. Continuity

La próxima CEND debe leer este checkpoint y continuar desde la posición de la pelota; no debe reconstruir nuevamente el dominio desde cero.
