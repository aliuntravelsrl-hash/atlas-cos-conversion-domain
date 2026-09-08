# ATLAS COS — Conversion Domain

## Estado

**COS Domain Repository · Live Representation · AS-IS / TO-BE / Continuous Learning**

Este repositorio representa el **dominio CONVERSION** del COS como un organismo vivo. No sustituye ni redefine los repositorios que materializan la operación; los sincroniza desde la perspectiva del comportamiento común del COS.

## Propósito

Mantener una representación navegable y trazable del ciclo de conversión mientras la pelota avanza por el sistema:

```text
DEMANDA
  ↓
ATRACCIÓN
  ↓
INTENCIÓN
  ↓
CALIFICACIÓN
  ↓
CONVERSIÓN / NEGOCIACIÓN
  ↓
COMPROMISO
  ↓
OBLIGACIÓN ECONÓMICA
  ↓
PAGO
  ↓
RESULTADO
  ↓
MEDICIÓN
  ↓
OUTCOME SIGNAL
  ↓
LEARNING
  ↓
MEJOR CONVERSIÓN
  ↺
```

El objetivo no es cambiar el núcleo del COS. El núcleo conserva el comportamiento; **el conocimiento, la evidencia y la navegación evolucionan**.

## Repositorios sincronizados

### Atlas Sales
Representa la estructura y los mecanismos comerciales del dominio: demanda, intención, calificación, oferta, negociación y compromiso.

### Hermes Commercial
Representa la ejecución comercial gobernada: recibe contexto, aplica estrategia e inteligencia, interactúa con el cliente y produce resultados.

### Atlas Sales MCP
Infraestructura técnica que habilita capacidades y herramientas para la ejecución comercial. No es autoridad constitucional ni propietario del dominio.

### Director / CCAMEL 360
Perspectiva soberana y de reconciliación 360. Observa el dominio completo y sus relaciones con el resto del COS; no sustituye la ejecución de los componentes.

## La pelota

La pelota **no es el agente**.

La pelota es el **contexto necesario para producir el siguiente resultado**.

Cada handoff debe poder responder:

```text
¿QUÉ RECIBE?
     ↓
¿QUÉ HACE?
     ↓
¿QUÉ ENTREGA?
     ↓
¿QUÉ EVIDENCIA QUEDA?
     ↓
¿QUÉ CONTEXTO RECIBE EL SIGUIENTE PUNTO?
```

## Cognitive + Learn Loop

Este repositorio materializa el dominio dentro del **Cognitive + Learn Loop**:

```text
OBSERVACIÓN
   ↓
EVIDENCIA
   ↓
REPRESENTACIÓN ESTRUCTURADA
   ↓
NAVEGACIÓN
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

Los hallazgos no deben quedar en una conversación. La observación y su evidencia pasan a una representación persistente y navegable conforme avanza la pelota.

## AS-IS → TO-BE → AS-IS

El dominio evoluciona continuamente:

```text
AS-ISₙ
  ↓
OBSERVACIÓN + EVIDENCIA
  ↓
COMPARABILIDAD
  ↓
DELTA
  ↓
GAP / EVO
  ↓
TO-BE
  ↓
DIRECTOR / AUTHORIZATION
  ↓
GOVERNED BUILD
  ↓
EXECUTION
  ↓
VALIDATION
  ↓
ADOPTION
  ↓
AS-ISₙ₊₁
  ↺
```

Un estado nuevo **nace del estado anterior**. La representación vigente no sustituye la genealogía.

## Genealogía y trazabilidad

Cada cambio relevante debe conservar su relación con:

- estado AS-IS que lo originó;
- observación;
- evidencia física;
- delta identificado;
- decisión o EVO correspondiente;
- autorización cuando aplique;
- TO-BE resultante;
- build / ejecución;
- validación;
- adopción;
- nuevo AS-IS.

La historia debe permitir recorrer tanto **hacia atrás** (genealogía) como **hacia adelante** (trazabilidad).

## Checkpoints

Los checkpoints son puntos de congelación del conocimiento navegable del dominio. No son simples informes de chat.

Cada checkpoint debe responder como mínimo:

1. ¿Dónde estaba el dominio?
2. ¿Qué observamos?
3. ¿Qué evidencia lo demuestra?
4. ¿Qué comportamiento era esperado?
5. ¿Qué comportamiento AS-IS fue encontrado?
6. ¿Qué coincide?
7. ¿Qué DELTA quedó registrado?
8. ¿Dónde quedó la pelota?
9. ¿Cuál es la siguiente ruta navegable?

## Regla de Drill

Durante el Drill:

```text
COMPORTAMIENTO ESPERADO
        ↓
REPRESENTACIÓN
        ↓
COMPORTAMIENTO REAL
        ↓
COMPARAR
        ↓
COINCIDE ─────→ BASELINE
        │
        └──────→ DELTA
```

Los **DELTA** se registran durante esta fase. La resolución estructural de un GAP / EVO pertenece a la fase posterior correspondiente y no se anticipa durante la observación.

## CEND

La entrada en frío ya no debe iniciar una arqueología indiscriminada.

```text
CEND
 ↓
IDENTIDAD
 ↓
ESTADO ACTUAL
 ↓
RUTA PERSISTIDA
 ↓
NAVEGACIÓN
 ↓
PELOTA
 ↓
OBSERVACIÓN
 ↓
EVIDENCIA
 ↓
ACTUALIZACIÓN DEL ORGANISMO
 ↓
SIGUIENTE PUNTO
```

**CEND reanuda el organismo; no descubre nuevamente su ruta.**

## Principios

- El COS mantiene un núcleo estable.
- Macro y Micro heredan el mismo comportamiento; cambia el conocimiento contextual.
- Los componentes existentes se sincronizan; no se duplican innecesariamente.
- Repositorio de dominio ≠ agente ≠ runtime ≠ autoridad.
- Evidencia física precede a la inferencia.
- UNKNOWN / NOT FOUND no significa NOT EXISTS.
- Los agentes ejecutan; la autoridad constitucional permanece en el Director/COS.
- El aprendizaje busca **mejor calidad y mayor velocidad sin sacrificar calidad**.
- La velocidad está subordinada a la calidad.
- Cada cambio debe conservar genealogía y trazabilidad.
- La sesión puede terminar; el organismo persistido no.

## Relación con el COS

Este repositorio es una representación de dominio. La autoridad constitucional continúa en `atlas-cos-v1`. Los repositorios operativos siguen siendo los propietarios de su código y ejecución.

El dominio CONVERSION sirve como plano de navegación y reconciliación para observar cómo esos componentes realizan un mismo comportamiento del COS.

## Estructura inicial

```text
atlas-cos-conversion-domain/
├── README.md
├── DOMAIN-MAP.md
├── AS-IS/
│   ├── README.md
│   ├── atlas-sales.md
│   ├── hermes-commercial.md
│   ├── atlas-sales-mcp.md
│   └── ccamel-360.md
├── BEHAVIOR/
│   ├── README.md
│   └── conversion-loop.md
├── SYNC/
│   ├── README.md
│   └── synchronization-map.md
├── EVIDENCE/
│   ├── README.md
│   └── evidence-index.md
├── CHECKPOINTS/
│   ├── README.md
│   └── CHECKPOINT-CONVERSION-DOMAIN-001.md
├── DELTAS/
│   ├── README.md
│   └── delta-register.md
├── LEARNING/
│   ├── README.md
│   └── learning-register.md
├── TO-BE/
│   ├── README.md
│   └── future-state.md
└── GENEALOGY/
    ├── README.md
    └── change-lineage.md
```

## Estado inicial

Este repositorio comienza como la representación persistente del **CONVERSION DOMAIN** y continuará evolucionando mediante Drill, evidencia, checkpoints y aprendizaje. No presupone que toda la cadena E2E esté demostrada; cada tramo será reconciliado contra AS-IS real.
