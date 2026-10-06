# 05 — Database

## Motor

MySQL.

La base se administra mediante Entity Framework Core.

## Entidades

### Usuario

Campos conceptuales:

```text
Id
Nombre
Apellido
Email
PasswordHash
Rol
Avatar
SucursalId nullable
Activo
```

Relación:

```text
Sucursal 1:N Usuario
```

### Sucursal

```text
Id
Nombre
Direccion
Telefono
Activa
```

Relaciones:

```text
Sucursal 1:N Usuario
Sucursal 1:N Stock
Sucursal 1:N Venta
```

### Categoria

```text
Id
Nombre
Descripcion
Activa
```

Relación:

```text
Categoria 1:N Producto
```

### Producto

```text
Id
Nombre
Descripcion
Codigo
Precio
Activo
CategoriaId
```

Relaciones:

```text
Categoria 1:N Producto
Producto 1:N Stock
Producto 1:N DetalleVenta
```

No se incluye imagen de producto.

### Stock

```text
Id
ProductoId
SucursalId
Cantidad
StockMinimo
```

Restricción:

```text
UNIQUE(ProductoId, SucursalId)
```

Esto evita dos registros de stock para el mismo producto en la misma sucursal.

### Venta

Campos conceptuales:

```text
Id
Fecha
Total
SucursalId
UsuarioId
Estado
ArchivoAdjunto
```

`ArchivoAdjunto` es opcional.

`Estado` permite conservar ventas anuladas sin eliminarlas.

Relaciones:

```text
Sucursal 1:N Venta
Usuario 1:N Venta
Venta 1:N DetalleVenta
```

### DetalleVenta

```text
Id
VentaId
ProductoId
Cantidad
PrecioUnitario
Subtotal
```

Relaciones:

```text
Venta 1:N DetalleVenta
Producto 1:N DetalleVenta
```

## Diagrama conceptual

```text
Sucursal
   │
   ├──────< Usuario
   │
   ├──────< Stock >──── Producto >──── Categoria
   │                       │
   └──────< Venta ────< DetalleVenta
              │
              └──── ArchivoAdjunto
```

## Reglas de integridad

- Foreign Keys para relaciones.
- Restricción única Producto + Sucursal en Stock.
- Cantidad de Stock >= 0.
- Cantidad de DetalleVenta > 0.
- Precio y subtotal no deben aceptar valores inválidos.
- Una Venta debe tener al menos un DetalleVenta al confirmarse.

## Migraciones

El esquema debe evolucionar mediante EF Core Migrations.

No modificar la base manualmente y después olvidar reflejar el cambio en el modelo/migración.

## Seed inicial

El proyecto puede tener datos iniciales mínimos para desarrollo:

- un Administrador;
- uno o más Empleados;
- una o más Sucursales;
- categorías y productos de prueba.

Las credenciales de desarrollo no deben utilizarse como credenciales reales.

## Entorno

La cadena de conexión debe provenir de configuración/variables de entorno.

No colocar credenciales reales en Git.
