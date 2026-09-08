# Synchronization Map

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
ATLAS SALES      HERMES COMMERCIAL
   │                   │
   └─────── SYNC ──────┘
           │
           ↓
      SALES MCP
           │
           ↓
      NEXT RESULT
```

## Sync invariant

Los componentes no tienen que compartir implementación. Deben poder recibir y producir el contexto requerido por el siguiente punto del loop.

## Evidence rule

Cada relación del mapa será marcada según evidencia real: VERIFIED, PARTIAL, UNKNOWN o NOT FOUND en el alcance investigado.