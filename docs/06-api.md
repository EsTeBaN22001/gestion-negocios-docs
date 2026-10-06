# 06 — API

## Convenciones

La API será REST.

Base conceptual:

```text
/api
```

La ruta exacta puede organizarse por Controller.

## Autenticación

```http
POST /api/auth/login
```

Entrada conceptual:

```json
{
  "email": "usuario@example.com",
  "password": "..."
}
```

Respuesta exitosa:

```json
{
  "token": "...",
  "expiresAt": "...",
  "user": {
    "id": 1,
    "nombre": "...",
    "apellido": "...",
    "rol": "Empleado",
    "sucursalId": 1
  }
}
```

## Productos

Conceptualmente:

```http
GET    /api/productos
GET    /api/productos/{id}
POST   /api/productos
PUT    /api/productos/{id}
DELETE /api/productos/{id}
```

Parámetros de lista:

```text
page
pageSize
search
sortBy
sortDirection
```

`sortBy` y `sortDirection` son opcionales. Si se implementan, deben utilizar una lista blanca de campos permitidos y no aceptar expresiones arbitrarias.

## Categorías

```text
GET
GET /{id}
POST
PUT /{id}
DELETE /{id}
```

## Sucursales

```text
GET
GET /{id}
POST
PUT /{id}
DELETE /{id}
```

## Usuarios

```text
GET
GET /{id}
POST
PUT /{id}
```

El diseño definitivo puede separar endpoints de administración y perfil propio.

## Stock

```text
GET /api/stock
GET /api/stock/{id}
POST /api/stock
PUT /api/stock/{id}
```

El backend debe aplicar el filtro de sucursal correspondiente.

## Ventas

```text
GET /api/ventas
GET /api/ventas/{id}
POST /api/ventas
POST /api/ventas/{id}/anular
```

La creación de una venta debe validar stock y utilizar transacción.

## Paginación

Respuesta estándar:

```json
{
  "items": [],
  "page": 1,
  "pageSize": 10,
  "totalItems": 100,
  "totalPages": 10
}
```

## HTTP status

Utilizar códigos HTTP estándar:

```text
200 OK
201 Created
204 No Content
400 Bad Request
401 Unauthorized
403 Forbidden
404 Not Found
409 Conflict
422 Unprocessable Entity (solo si existe una razón clara para usarlo)
500 Internal Server Error
```

No inventar códigos personalizados.

## Errores

Preferir el mecanismo estándar de errores de ASP.NET Core, especialmente `ProblemDetails`, salvo que exista una razón documentada para otra estructura.

## Autorización

Los endpoints sensibles deben utilizar:

```csharp
[Authorize]
```

o:

```csharp
[Authorize(Roles = "Administrador")]
```

La autorización no debe depender solamente de Angular.

## Swagger

Todos los endpoints deben estar documentados mediante Swagger/OpenAPI de forma razonable.

Los endpoints protegidos deben poder probarse enviando el JWT.

## Búsquedas

Las búsquedas se procesan en el backend.

Ejemplo:

```http
GET /api/productos?search=coca&page=1&pageSize=10
```

El backend consulta solamente los resultados necesarios.
