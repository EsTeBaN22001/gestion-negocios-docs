# ADR-005 — File Storage

## Estado

Aceptado.

## Decisión

Los archivos se almacenarán en el filesystem del backend.

Se utilizarán:

```text
wwwroot/uploads/avatars/
wwwroot/uploads/ventas/
```

La base almacena la referencia al archivo.

## Motivo

Es más simple para el proyecto que guardar archivos binarios directamente en MySQL.

## Consecuencia

Docker debe utilizar un volumen persistente para uploads cuando corresponda.
