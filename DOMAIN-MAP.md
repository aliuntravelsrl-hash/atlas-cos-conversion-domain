# Conversion Domain — Domain Map

## Purpose

Mapa vivo del dominio CONVERSION y de los repositorios que lo materializan.

```text
                         COS
                          │
                  CONVERSION DOMAIN
                          │
        ┌─────────────────┼─────────────────┐
        ↓                 ↓                 ↓
   ATLAS SALES      HERMES COMMERCIAL   SALES MCP
        │                 │                 │
        └──────────────── SYNC ─────────────┘
                          │
                    COMPROMISO
                          │
                    OBLIGACIÓN
                          │
                        PAGO
                          │
                      RESULTADO
                          │
                   CCAMEL 360
                          │
                     LEARNING
```

## Domain boundary

### In scope

- intención y calificación;
- oferta y negociación;
- compromiso;
- obligación económica;
- transición a pago;
- evidencia de conversión;
- resultados y medición;
- aprendizaje derivado del comportamiento de conversión;
- sincronización entre los componentes que materializan el dominio.

### Out of scope

- redefinir la Constitución del COS;
- sustituir los repositorios operativos;
- autorizar cambios constitucionales;
- crear capacidades nuevas sin el proceso gobernado correspondiente;
- resolver DELTAS durante la fase de Drill.

## Navigation rule

La pelota se representa como contexto sincronizado, no como un agente:

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

El contenido exacto de la pelota se actualizará conforme la evidencia AS-IS lo demuestre.
