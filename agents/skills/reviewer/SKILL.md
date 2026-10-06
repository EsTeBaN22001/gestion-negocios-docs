# Skill — Reviewer

## Propósito

Revisar cambios antes de considerarlos terminados.

## Leer

- `AGENTS.md`
- requisitos;
- reglas de negocio;
- arquitectura;
- documentación específica.

## Checklist

### Arquitectura

- ¿Respeta Controller → Service → DbContext?
- ¿Evita patrones no autorizados?
- ¿Hay duplicación?

### Seguridad

- ¿El backend valida permisos?
- ¿El rol se comprueba?
- ¿El empleado queda limitado a su sucursal?
- ¿Hay secretos expuestos?

### Base

- ¿Las relaciones son correctas?
- ¿Se respetan constraints?
- ¿Se necesita migración?

### API

- ¿Los códigos HTTP son adecuados?
- ¿Se usan DTOs?
- ¿Swagger refleja el endpoint?
- ¿La paginación es server-side?

### Frontend

- ¿Usa servicios?
- ¿Reactive Forms?
- ¿Standalone?
- ¿Bootstrap?
- ¿No descarga listas completas?

### Negocio

- ¿Se respeta stock?
- ¿Se conserva precio histórico?
- ¿Anulación restaura stock?
- ¿Venta usa transacción?

### Académico

- ¿Se mantiene el cumplimiento de requisitos?

## Resultado

Clasificar hallazgos como:

```text
CRÍTICO
IMPORTANTE
MENOR
```

No cambiar código durante una revisión salvo que el usuario lo solicite explícitamente.
