# 04 — Backend

## Tecnología

- ASP.NET Core .NET 8
- C#
- Entity Framework Core
- MySQL
- JWT
- Swagger/OpenAPI

## Estructura

```text
Controllers/
Services/
Models/
DTOs/
Data/
Middleware/
Helpers/
Migrations/
wwwroot/
```

## Flujo

```text
HTTP Request
    ↓
Controller
    ↓
Service
    ↓
DbContext
    ↓
EF Core
    ↓
MySQL
```

## Controllers

Los Controllers deben ser delgados.

Ejemplo conceptual:

```text
ProductosController
    ↓
ProductosService
```

El Controller no debe contener reglas complejas como:

- descuento de stock;
- cálculo de permisos por sucursal;
- creación coordinada de venta y detalles.

Eso pertenece al Service.

## Services

Los Services contienen la lógica de negocio.

Ejemplos:

- `AuthService`
- `ProductoService`
- `StockService`
- `VentaService`
- `UsuarioService`

No es obligatorio crear un Service para cada entidad si no aporta valor, pero debe existir una separación clara de responsabilidades.

## DTOs

Usar DTOs para:

- creación;
- actualización;
- respuesta;
- login;
- paginación.

Ejemplo:

```text
ProductoCreateDto
ProductoUpdateDto
ProductoResponseDto
```

## Validación

Validar:

1. formato;
2. datos requeridos;
3. reglas de negocio;
4. permisos;
5. pertenencia a sucursal.

La validación de frontend no reemplaza la del backend.

## EF Core

EF Core será el mecanismo principal de persistencia.

No escribir SQL manual para operaciones normales.

## Migraciones

Las modificaciones de esquema se realizarán mediante migraciones:

```bash
dotnet ef migrations add NombreMigracion
dotnet ef database update
```

Los agentes deben revisar migraciones existentes antes de crear nuevas.

## Transacciones

Las operaciones de venta que afecten:

- Venta;
- DetalleVenta;
- Stock;

deben realizarse de forma atómica.

## Swagger

Swagger/OpenAPI debe estar disponible en desarrollo para inspeccionar y probar endpoints.

## Dependencias

No agregar paquetes innecesarios.

Antes de instalar una dependencia, comprobar si .NET 8, ASP.NET Core o EF Core ya ofrecen una solución suficiente.
