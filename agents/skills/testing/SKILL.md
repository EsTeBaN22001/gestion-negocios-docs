# Skill — Testing

## Leer antes

- `docs/12-testing.md`
- `docs/02-business-rules.md`

## Objetivo

Probar comportamiento crítico sin sobreingeniería.

## Prioridades

1. Login.
2. Autorización.
3. Filtro por sucursal.
4. CRUD principal.
5. Venta.
6. Stock.
7. Anulación.
8. Archivos.
9. Paginación.
10. Búsqueda.

## Regla

No crear una suite enorme si el cambio no lo necesita.

Después de cambios importantes, al menos:

- compilar;
- ejecutar flujo afectado;
- verificar respuesta HTTP;
- verificar persistencia si corresponde.
