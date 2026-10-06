# 02 — Business Rules

## Usuarios

1. Un usuario tiene un rol.
2. Los roles válidos son `Administrador` y `Empleado`.
3. Un Empleado debe pertenecer a una Sucursal.
4. Un Administrador puede tener `SucursalId = null`.
5. Un Empleado no puede cambiar su propia sucursal.
6. El usuario puede modificar su propia información permitida.
7. El Administrador puede administrar usuarios.

## Sucursales

1. Una sucursal puede tener muchos empleados.
2. Una sucursal puede tener stock de muchos productos.
3. Una sucursal puede tener muchas ventas.
4. Solo Administrador administra sucursales.

## Categorías

1. Un producto pertenece a una categoría.
2. Una categoría puede tener muchos productos.
3. Solo Administrador administra categorías.

## Productos

1. Cada producto pertenece a una categoría.
2. El precio pertenece al producto.
3. El precio histórico de una venta NO debe depender del precio actual del producto.
4. Solo Administrador administra productos.
5. No se necesita imagen de producto.

## Stock

1. El stock pertenece simultáneamente a un producto y una sucursal.
2. Un producto puede tener diferentes cantidades en diferentes sucursales.
3. No puede existir más de un registro de Stock para la combinación Producto + Sucursal.
4. La cantidad no puede ser negativa.
5. El Administrador puede realizar ajustes manuales.
6. Una venta confirmada reduce el stock.
7. Una venta anulada devuelve al stock las cantidades que había descontado.

## Ventas

1. Una venta pertenece a una sucursal.
2. Una venta pertenece al usuario que la realizó.
3. Una venta debe tener al menos un DetalleVenta.
4. No se puede confirmar una venta si no hay stock suficiente.
5. La venta y sus detalles deben guardarse de manera consistente.
6. El descuento de stock debe ocurrir dentro de una transacción.
7. Una venta anulada no se elimina físicamente.
8. Al anular una venta, se restauran las cantidades de sus detalles.
9. Una venta puede tener un archivo adjunto opcional.
10. `PrecioUnitario` de DetalleVenta conserva el precio que existía al momento de la venta.

## Sucursal del usuario

Para un Empleado:

```text
JWT
 ↓
Usuario
 ↓
SucursalId
 ↓
filtrado obligatorio por sucursal
```

El Empleado no debe poder enviar desde el frontend un `SucursalId` diferente para acceder a otra sucursal.

El backend debe determinar la sucursal desde el usuario autenticado cuando corresponda.

## Administrador

El Administrador puede operar sobre todas las sucursales, respetando las reglas generales.

## Regla de consistencia

Si una operación modifica múltiples datos relacionados, debe utilizarse una transacción cuando sea necesario para garantizar atomicidad.
