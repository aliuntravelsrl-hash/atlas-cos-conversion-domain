# EVIDENCE-CONVERSION-002 — FRONT G Runtime Evidence & Tool Invocation Trace

**Fecha:** 09 Sep 2026 · 08:30 (Local Time)  
**Dominio:** CONVERSION (Hermes Commercial Runtime / Capability Invocations)  
**Estado:** VERIFIED / CONCLUSIÓN EPISTÉMICA AUDITADA  
**Investigador / Auditor:** Antigravity (ATLAS-TECH / Curator Constitucional)  
**Autoridad Soberana:** Director General Aldo Hilario  

---

## 1. Cadena de Evidencia (OBSERVACIÓN → FUENTE → EVIDENCIA → CONCLUSIÓN)

### Observación:
Determinar si en el historial de ejecución real de Hermes Commercial en VPS2 (`hermes-agent-dpkf-hermes-agent-1`) existe evidencia física de que las decisiones comerciales emitieron llamadas a herramientas (`tool_calls`) hacia capacidades canónicas (`calcular_cotizacion`, `buscar_hoteles`, `atlas-sales-mcp`), o si la operación comercial histórica se ejecutó como generación de texto/prompting sin materialización de llamadas de herramientas estructuradas.

---

### Fuentes Primarias Inspeccionadas en VPS2:
1. **Directorio de Sesiones:** `/opt/data/sessions/*.json` (3,425 archivos JSON analizados).
2. **Base de Datos Principal del Agente:** `/opt/data/state.db` (4.1 GB, 73,897 mensajes históricos, 10,732 sesiones).
3. **Tablas de Despacho:** `/opt/data/kanban.db` (0 tareas históricas persistidas).
4. **Tabla de Prompts de Sistema:** `system_prompts` en `state.db` (154 prompts versionados).

---

### Evidencia Recopilada:

#### 1. Escaneo Total de 3,425 Archivos de Sesión (`/opt/data/sessions/`):
- **Coincidencias de Palabras Clave:**
  - `calcular_cotizacion`: 12 archivos
  - `buscar_hoteles`: 14 archivos
  - `consultar_y_registrar`: 2 archivos
  - `atlas-sales-mcp`: 32 archivos
  - `cotizacion`: 15 archivos
  - `cotizar`: 14 archivos
- **Invocaciones Reales de Herramientas (`tool_calls` estructurados en JSON):**
  - Distinct tools invocadas: **0**
  - Relevant commercial tool call instances: **0**
- **Naturaleza de los Archivos con Coincidencias:**
  - Corresponden a dumps de errores de peticiones/cron (`request_dump_*.json`), donde los términos aparecen dentro del texto del prompt o historial enviado al LLM, no como eventos de ejecución RPC o retorno de herramientas.

#### 2. Inspección de 73,897 Mensajes en `state.db`:
- Los registros donde aparecen `atlas-sales-mcp` o `calcular_cotizacion` corresponden a consultas del usuario auditando al agente (ej. IDs 346, 380, 431).
- **Respuestas registradas del propio Hermes Commercial (IDs 386, 412):**
  > *"La sesión actual no tiene acceso terminal/browser directo — solo tengo las tools de mensajería."*  
  > *"❌ Sesión sin herramientas de terminal/file. Esta sesión del agente no tiene acceso a terminal, read_file, ni execute_code disponibles."*

#### 3. Prompts de Sistema y Contrato SOUL (`system_prompts`):
- Los hashes (ej. `24a739d14f15`, `b6a0854b1e83`) contienen la especificación formal del contrato SOUL v2:
  `Identidad: Orquestador Comercial — F3-ATRACCION, Aliun Travel SRL`
  `Mis herramientas: atlas-sales-mcp (14 tools) · WF-COTIZACION`
- Sin embargo, las herramientas estaban listadas como directrices de contexto en el prompt, mientras el runtime del contenedor carecía del socket MCP cliente conectado activamente para resolver el ciclo de llamadas `tool_call -> MCP -> RPC`.

---

## 2. Conclusión Epistémica de FRONT G

| Eje | Estado Demostrado |
|---|---|
| **Intención & Contrato (SOUL v2)** | ✅ Formalmente definido (`F3-ATRACCION`, rol comercial, referencia a `atlas-sales-mcp`). |
| **Ruteo & Prompting** | ✅ Activo y documentado en `ROUTING.md` (6 departamentos, directrices de ventas). |
| **Lineage de Invocación RPC Real** | ❌ **0 invocaciones MCP registradas en el runtime histórico.** Hermes Commercial operó exclusivamente mediante generación textual de lenguaje natural sin invocar de forma material el motor canónico `calcular_cotizacion`. |

### Veredicto de Gobernanza:
La frontera de FRONT G queda delimitada con exactitud científica:
**No hubo falla en la ejecución de la herramienta porque la herramienta nunca fue llamada por el runtime histórico.** La cotización operó como recomendación conversacional asistida por prompt, marcando la necesidad de consolidar el nuevo pipeline HTTP Gateway (`WF-CHATWOOT-HERMES-v1`) con validación canónica de precios antes del cierre de reserva.
