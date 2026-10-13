# 13 — Project Progress

Este archivo es mantenido por los agentes y por el desarrollador.

Los agentes pueden actualizarlo después de completar trabajo verificable.

## Estado general

- [x] Idea del sistema aprobada por profesor
- [x] Entidades principales definidas
- [x] Roles definidos
- [x] Reglas principales definidas
- [x] Stack definido
- [x] Arquitectura general definida
- [x] Crear repositorio backend
- [x] Crear repositorio frontend
- [x] Crear solución ASP.NET Core
- [x] Configurar EF Core
- [x] Configurar MySQL
- [x] Crear migración inicial
- [x] Crear Docker Compose
- [x] Crear proyecto Angular
- [x] Configurar Bootstrap
- [x] Completar Fase 0 y checklist de infraestructura
- [x] Implementar autenticación
- [ ] Implementar usuarios
- [ ] Implementar sucursales
- [ ] Implementar categorías
- [ ] Implementar productos
- [ ] Implementar stock
- [ ] Implementar ventas
- [ ] Implementar anulación de ventas
- [ ] Implementar archivos
- [ ] Implementar paginación
- [ ] Implementar búsquedas
- [x] Implementar Swagger (base de infraestructura)
- [ ] Pruebas funcionales
- [ ] Revisión académica
- [ ] Preparar entrega

## Regla

No marcar una tarea como terminada solo porque el código fue escrito.

Debe estar implementada y verificada.

## Registro de actualizaciones

```text
Fecha: 2026-10-06
Tarea: Fase 0 — Infraestructura y arranque (P0-01 a P0-09)
Implementación:
  - Backend ASP.NET Core 8 Web API estructurado con Data, Models, Controllers, appsettings por ambiente.
  - Pomelo MySQL 8.0 y EF Core 8 configurados con retry policy.
  - Entidades base creadas según docs/05-database.md (Usuario, Sucursal, Categoria, Producto, Stock, Venta, DetalleVenta) con Fluent API en ApplicationDbContext.
  - Migración inicial "InitialCreate" generada exitosamente con dotnet-ef.
  - Migración automática en startup y endpoint de verificación técnica /api/health y /api/health/db.
  - Swagger/OpenAPI habilitado en Development.
  - Frontend Angular 18 (Standalone Components) creado con Bootstrap 5 y Bootstrap Icons.
  - Componente inicial HomeComponent con verificación de estado de API y MySQL vía ApiService.
  - Entornos Angular (environment.ts / environment.prod.ts) y rutas base configuradas.
  - Docker Compose orquestando backend, frontend (Nginx multi-stage) y MySQL 8.0 con healthcheck y volumen persistente.
  - Repositorios Git independientes en backend y frontend con ramas 'master' (estable) y 'develop' (activa), y commits iniciales limpios.
Verificación:
  - Compilación de backend: dotnet build exitoso con 0 errores y 0 advertencias.
  - Migración EF Core: dotnet dotnet-ef migrations add InitialCreate completada exitosamente.
  - Compilación de frontend: npm run build de Angular completado con éxito (dist/gestion-negocios/browser).
Pendientes para Fase 1:
  - Base de datos y modelo de dominio completados en esta fase.
```

```text
Fecha: 2026-10-08
Tarea: Fase 1 — Base de datos y modelo de dominio
Implementación:
  - Verificación y ajuste del modelo de dominio de 7 entidades: Usuario, Sucursal, Categoria, Producto, Stock, Venta, DetalleVenta.
  - Corrección de compatibilidad en ApplicationDbContext, migración InitialCreate y Snapshot: ajuste de CURRENT_TIMESTAMP a CURRENT_TIMESTAMP(6) para datetime(6) de MySQL 8.0 en Usuario.FechaCreacion y Venta.Fecha.
  - Configuración Fluent API de relaciones:
      * Sucursal 1:N Usuario (Restrict, SucursalId nullable para Administrador)
      * Sucursal 1:N Stock (Restrict)
      * Sucursal 1:N Venta (Restrict)
      * Categoria 1:N Producto (Restrict)
      * Producto 1:N Stock (Restrict)
      * Producto 1:N DetalleVenta (Restrict)
      * Usuario 1:N Venta (Restrict)
      * Venta 1:N DetalleVenta (Cascade)
  - Restricciones de integridad y unicidad configuradas:
      * Index único en Categoria.Nombre
      * Index único en Producto.Codigo
      * Index único compuesto en Stock (ProductoId, SucursalId)
      * Index único en Usuario.Email
      * Precisión monetaria decimal(18,2) en precios, subtotales y totales
  - Sincronización completa de modelo EF Core: dotnet ef migrations has-pending-model-changes confirma 0 cambios pendientes.
  - Aplicación exitosa de la migración InitialCreate tanto en base de datos local de desarrollo (gestion_negocios_dev) como en base de datos de producción/Docker (gestion_negocios).
Verificación:
  - Compilación de backend: dotnet build exitoso con 0 errores y 0 advertencias.
  - EF Core: Modelo sincronizado sin cambios pendientes.
  - Migración aplicada: Tabla __EFMigrationsHistory registra 20261006212234_InitialCreate.
  - Verificación en MySQL: 7 tablas creadas con PKs auto-incrementables, tipos de datos, FKs y unique constraints comprobados.
  - Pruebas SQL funcionales: Inserción de entidades válidas, verificación de fallo por clave foránea inválida, verificación de fallo por restricción de unicidad duplicada, y verificación de borrado en cascada de DetallesVenta al eliminar Venta.
  - Docker Compose: Todos los contenedores (backend, frontend, mysql) activos y saludables; endpoints /api/health y /api/health/db responden 200 OK.
Pendientes para Fase 2:
  - Autenticación JWT, registro/login y módulo de gestión de usuarios.
```

```text
Fecha: 2026-10-13
Tarea: Fase 2 — Autenticación y autorización completa
Implementación:
  - Backend ASP.NET Core:
      * Integración de Microsoft.AspNetCore.Authentication.JwtBearer con validación de clave simétrica HMAC-SHA256, Issuer, Audience, Lifetime y ClockSkew nulo.
      * PasswordHasher<Usuario> registrado en DI para hash y verificación segura de contraseñas.
      * AuthService implementado con Controller -> Service -> DbContext y DTOs con mapeo manual (LoginRequestDto, LoginResponseDto, UserDto).
      * Claims estándar: NameIdentifier (ID), Email, Name, Role, Jti, y claim condicional "sucursalId" para Empleados.
      * AuthController implementado con endpoints:
          - POST /api/auth/login: login público, validación ModelState, respuesta 401 genérica sin revelar si falló email o password.
          - GET /api/auth/me: protegido con [Authorize], devuelve UserDto sin exponer PasswordHash.
          - GET /api/auth/admin-check: restringido con [Authorize(Roles = "Administrador")].
      * Swagger/OpenAPI configurado con soporte para JWT Bearer Authentication (SecurityDefinition y SecurityRequirement).
      * DataSeeder seguro: genera sucursal y usuarios iniciales de desarrollo (Administrador sin sucursal y Empleado con sucursal) utilizando PasswordHasher con credenciales configurables vía appsettings y variables de entorno.
      * Suite automatizada de pruebas backend en tests/GestionNegocios.Api.Tests con 15 pruebas unitarias y de validación JWT (xUnit + InMemory EF Core).
  - Frontend Angular:
      * Core Models: interfaces User, LoginRequest, LoginResponse.
      * AuthService: gestión reactiva con BehaviorSubject (currentUser$), persistencia segura en localStorage, verificación de expiración de token y método logout().
      * Interceptor HTTP (authInterceptor): adjunta Bearer token a solicitudes contra la API y captura errores 401 para cerrar sesión de forma automática.
      * Guards de navegación: authGuard para rutas privadas y roleGuard para verificación de roles en Angular.
      * Componente de Login (LoginComponent): formulario reactivo con validaciones, mensajes comprensibles en Bootstrap, spinner de carga y prevención de re-envío.
      * Panel de verificación en HomeComponent y barra de navegación en AppComponent que refleja el estado de sesión (datos, rol, sucursal, logout).
      * Suite automatizada de pruebas frontend con Karma y ChromeHeadless (16 pruebas aprobadas).
Verificación:
  - Backend Build: dotnet build con 0 errores y 0 advertencias.
  - Backend Tests: 15/15 pruebas unitarias y de validación JWT aprobadas (dotnet test).
  - Frontend Build: ng build completado exitosamente.
  - Frontend Tests: 16/16 pruebas unitarias de Karma/ChromeHeadless aprobadas.
  - Verificación API en vivo contra MySQL (gestion_negocios_dev):
      * Login con Administrador exitoso (200 OK con token y UserDto sin PasswordHash).
      * Login con Empleado exitoso (200 OK con claim sucursalId).
      * Login con contraseña incorrecta rechazado (401 Unauthorized con ProblemDetails genérico).
      * Login con usuario inexistente rechazado (401 Unauthorized con ProblemDetails genérico).
      * Login con usuario inactivo rechazado (401 Unauthorized con ProblemDetails genérico).
      * Endpoint protegido sin token rechazado (401 Unauthorized).
      * Endpoint protegido con token válido aprobado (200 OK con UserDto).
      * Token alterado / firma inválida rechazado (401 Unauthorized).
      * Token vencido rechazado tanto por middleware en vivo como por prueba de validación (401 Unauthorized).
      * Restricción por rol comprobada: Administrador accede a /api/auth/admin-check (200 OK) y Empleado es rechazado (403 Forbidden).
  - Docker Compose: docker compose build de imágenes backend y frontend completado exitosamente.
Pendientes para Fase 3:
  - Módulos de gestión (CRUD): Usuarios, Sucursales y Categorías.
```

## Decisiones pendientes

Ninguna. La implementación de Fase 2 cumple estrictamente con docs/08-authentication.md, docs/06-api.md, docs/02-business-rules.md y ADR-003.

