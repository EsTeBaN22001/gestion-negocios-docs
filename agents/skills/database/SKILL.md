# Skill — Database

## Leer antes

- `docs/05-database.md`
- `docs/02-business-rules.md`
- `docs/03-architecture.md`

## Reglas

- EF Core es la fuente de persistencia.
- MySQL es el motor.
- Usar migraciones.
- No SQL manual para operaciones normales.
- No duplicar relaciones.
- Respetar foreign keys.
- Respetar restricciones únicas.
- Evitar datos redundantes.

## Cambios de esquema

Antes de modificar entidades:

1. Revisar relaciones.
2. Revisar reglas.
3. Modificar modelo.
4. Crear migración.
5. Revisar migración.
6. Aplicar migración.
7. Verificar funcionamiento.

## Stock

Mantener única la combinación:

```text
ProductoId + SucursalId
```

## Ventas

No romper la relación:

```text
Venta → DetalleVenta → Producto
```

## Agente

Nunca borrar o recrear migraciones existentes sin una razón explícita.
