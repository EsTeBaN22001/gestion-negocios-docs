# 01 — Requirements

## 1. Requisitos funcionales

### Autenticación

- Login de usuarios.
- Autenticación mediante JWT.
- Roles Administrador y Empleado.
- Protección de endpoints mediante `[Authorize]`.
- Restricción de funcionalidades según rol.

### Usuarios

- Crear usuarios.
- Modificar usuarios.
- Consultar usuarios.
- Activar/desactivar usuarios según las reglas definidas.
- Asignar rol.
- Asignar sucursal a empleados.
- Avatar.
- Modificación del perfil propio.
- El usuario no puede cambiar su propia sucursal.

### Sucursales

- CRUD de sucursales.
- Solamente Administrador puede administrarlas.

### Categorías

- CRUD de categorías.
- Solamente Administrador puede administrarlas.

### Productos

- CRUD de productos.
- Cada producto pertenece a una categoría.
- Solamente Administrador administra productos.
- El precio lo administra el Administrador.

### Stock

- Stock por producto y sucursal.
- Consulta de stock.
- Paginación.
- Búsqueda.
- Ajuste manual por Administrador.
- No se permiten cantidades negativas.
- No se permiten duplicados Producto + Sucursal.

### Ventas

- Crear ventas.
- Una venta debe tener al menos un detalle.
- Una venta pertenece a una sucursal.
- Una venta registra al usuario que la realizó.
- Verificar stock antes de confirmar.
- Descontar stock automáticamente.
- Guardar precio unitario histórico.
- Adjuntar opcionalmente un archivo.
- Anular una venta.
- Al anular, devolver el stock.
- No borrar físicamente una venta anulada.

## 2. Requisitos técnicos

- Backend ASP.NET Core .NET 8.
- Entity Framework Core.
- MySQL.
- Angular.
- JWT.
- API REST.
- Swagger/OpenAPI.
- DTOs.
- Paginación server-side.
- Búsqueda server-side.
- Docker Compose.
- Repositorios GitHub separados para backend y frontend.

## 3. Frontend

El frontend utilizará Angular.

El requisito de interacción AJAX se implementará mediante llamadas HTTP asíncronas de Angular usando `HttpClient`.

No se utilizará Vue.

## 4. Archivos

El sistema debe tener:

- avatar de usuario;
- otro uso de archivos además del avatar.

El segundo uso será un archivo adjunto opcional asociado a una venta.

## 5. Regla de seguridad

La seguridad no depende de Angular.

El backend debe validar:

- identidad;
- rol;
- sucursal;
- permisos;
- reglas de negocio;
- datos recibidos.

Angular solamente mejora la experiencia del usuario.

## 6. Requisito de paginación

Las listas importantes deben paginarse en servidor.

No está permitido descargar toda la tabla para paginar en Angular.

## 7. Requisito de búsqueda

Las búsquedas deben realizarse en el servidor.

Especialmente para seleccionar entidades relacionadas.

## 8. Requisito de documentación

El repositorio final debe contener:

- README;
- diagrama ER/clases;
- documentación relevante;
- instrucciones de ejecución;
- documentación de API;
- información sobre requisitos académicos;
- colección Postman si se decide crearla para la entrega.
