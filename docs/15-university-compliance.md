# 15 — University Compliance

## Objetivo

Este documento permite verificar que el sistema cumple los requisitos académicos definidos para el proyecto.

## Requisito: ASP.NET Core

Implementación:

```text
Backend ASP.NET Core .NET 8
```

## Requisito: entidades relacionadas

El sistema posee más de cuatro entidades:

```text
Usuario
Sucursal
Categoria
Producto
Stock
Venta
DetalleVenta
```

## Requisito: relación 1:N

Ejemplos:

```text
Sucursal 1:N Usuario
Categoria 1:N Producto
Venta 1:N DetalleVenta
Producto 1:N Stock
```

## Requisito: Login

Implementación:

```text
POST /api/auth/login
JWT
```

## Requisito: Authorize

Implementación:

```csharp
[Authorize]
```

y restricciones de rol:

```csharp
[Authorize(Roles = "Administrador")]
```

## Requisito: roles

Roles:

```text
Administrador
Empleado
```

## Requisito: funcionalidad restringida

Ejemplos:

- Administración de usuarios: Administrador.
- Administración de sucursales: Administrador.
- Administración de categorías: Administrador.
- Administración de productos: Administrador.
- Ajuste manual de stock: Administrador.

## Requisito: avatar

`Usuario.Avatar`.

Los archivos se almacenan en filesystem.

## Requisito: uso adicional de archivos

`Venta.ArchivoAdjunto` opcional.

Esto permite adjuntar comprobantes/documentos relacionados con una venta.

## Requisito: ABM/CRUD con AJAX

El frontend se implementa con Angular.

Las operaciones utilizan `HttpClient`, es decir, comunicación HTTP asíncrona con la API.

No se utilizará Vue.

## Requisito: paginación server-side

Las listas se procesan con:

```text
Skip()
Take()
```

en el backend mediante EF Core.

## Requisito: búsqueda server-side

Las búsquedas se ejecutan mediante consultas API.

No se descarga la colección completa al frontend para filtrar.

## Requisito: selección de entidades relacionadas

Los formularios utilizan búsquedas HTTP para seleccionar entidades relacionadas.

Ejemplo:

```text
Buscar producto
↓
API
↓
resultados paginados
```

## Requisito: JWT/API

La aplicación posee API REST protegida mediante JWT.

## Swagger

Swagger/OpenAPI facilita la demostración de endpoints.

## Entrega

Antes de entregar, verificar:

- [ ] Repositorios Git correctos.
- [ ] README actualizado.
- [ ] Diagrama actualizado.
- [ ] Migraciones presentes.
- [ ] Docker Compose funcional.
- [ ] Usuarios de prueba.
- [ ] Roles de prueba.
- [ ] API funcional.
- [ ] Requisitos marcados como terminados.
- [ ] Pruebas funcionales realizadas.

## Nota

Este documento debe actualizarse si el profesor cambia o aclara algún requisito.
