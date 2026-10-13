# 08 — Authentication

## Estrategia

Autenticación propia del proyecto utilizando:

- JWT (`Microsoft.AspNetCore.Authentication.JwtBearer`);
- `PasswordHasher<Usuario>` (`Microsoft.AspNetCore.Identity.PasswordHasher<Usuario>`);
- Roles almacenados en la entidad `Usuario` (`Administrador` y `Empleado`).

No se utiliza ASP.NET Core Identity completo ni IdentityDbContext, respetando la arquitectura estándar `Controller -> Service -> DbContext`.

## Endpoints implementados

### 1. Iniciar sesión

```http
POST /api/auth/login
```

- **Acceso:** Público (`[AllowAnonymous]`).
- **Entrada (`LoginRequestDto`):**
  ```json
  {
    "email": "admin@gestionnegocios.local",
    "password": "Password123*"
  }
  ```
- **Respuesta exitosa (`200 OK`, `LoginResponseDto`):**
  ```json
  {
    "token": "eyJhbGciOi...",
    "expiresAt": "2026-10-13T23:16:00Z",
    "user": {
      "id": 1,
      "nombre": "Administrador",
      "apellido": "Sistema",
      "email": "admin@gestionnegocios.local",
      "rol": "Administrador",
      "sucursalId": null,
      "avatar": null
    }
  }
  ```
- **Respuesta ante credenciales incorrectas o usuario inactivo (`401 Unauthorized`, `ProblemDetails`):**
  ```json
  {
    "title": "Credenciales incorrectas",
    "status": 401,
    "detail": "El email o la contraseña son incorrectos o la cuenta se encuentra desactivada."
  }
  ```
  *Nota de seguridad:* No se revela si falló el email o la contraseña.
- **Respuesta ante datos inválidos (`400 Bad Request`):** Estándar de ASP.NET Core `ProblemDetails` con colección de errores.

### 2. Obtener identidad autenticada

```http
GET /api/auth/me
```

- **Acceso:** Autenticado (`[Authorize]`).
- **Encabezado:** `Authorization: Bearer <token>`
- **Respuesta exitosa (`200 OK`, `UserDto`):** Devuelve la información del usuario actual autenticado sin incluir nunca el `PasswordHash`.

### 3. Verificación de permisos de Administrador

```http
GET /api/auth/admin-check
```

- **Acceso:** Restringido a Administradores (`[Authorize(Roles = "Administrador")]`).
- **Respuesta exitosa (`200 OK`):** Para usuarios con rol `Administrador`.
- **Respuesta rechazada (`403 Forbidden`):** Para usuarios con rol `Empleado`.
- **Respuesta sin autenticación (`401 Unauthorized`):** Para solicitudes sin token o con token inválido/vencido.

## Claims del Token JWT

El JWT contiene exclusivamente los claims necesarios:

- `ClaimTypes.NameIdentifier` (`sub` / `nameid`): ID numérico del usuario.
- `ClaimTypes.Email`: Email del usuario.
- `ClaimTypes.Name` (`unique_name`): Nombre completo (`Nombre + Apellido`).
- `ClaimTypes.Role` (`role`): Rol del usuario (`Administrador` o `Empleado`).
- `sucursalId`: ID de la sucursal asignada (únicamente cuando `SucursalId` tiene valor, obligatorio para `Empleado`).
- `jti`: Identificador único de token (GUID).

## Configuración y Expiración

Variables de configuración en `appsettings.json` y variables de entorno:

| Variable | Configuración | Descripción |
|---|---|---|
| `Jwt:Key` | `Jwt__Key` | Clave simétrica de firma (mínimo 32 bytes). |
| `Jwt:Issuer` | `Jwt__Issuer` | Emisor del token (por defecto: `GestionNegociosApi`). |
| `Jwt:Audience` | `Jwt__Audience` | Audiencia permitida (por defecto: `GestionNegociosFrontend`). |
| `Jwt:DurationMinutes` | `Jwt__DurationMinutes` | Duración del token en minutos (por defecto: 60). |

Parámetros de validación en ASP.NET Core:
- `ValidateIssuerSigningKey = true`
- `ValidateIssuer = true`
- `ValidateAudience = true`
- `ValidateLifetime = true`
- `ClockSkew = TimeSpan.Zero`

## Almacenamiento seguro de contraseñas

Se utiliza `Microsoft.AspNetCore.Identity.PasswordHasher<Usuario>` registrado como singleton en el contenedor de dependencias:
- Genera hash criptográfico con PBKDF2 y salt aleatorio por usuario.
- Nunca se almacena ni se devuelve la contraseña en texto plano ni el hash en respuestas HTTP.

## Inicialización de Usuarios (Seed de Desarrollo)

`DataSeeder` inicializa datos mínimos en desarrollo si la tabla `Usuarios` está vacía:
- Crea `Sucursal Central` si no existen sucursales.
- Crea usuario `Administrador` (`SucursalId = null`).
- Crea usuario `Empleado` (`SucursalId = 1`).
- Las credenciales iniciales se leen de `Seed:AdminEmail`, `Seed:AdminPassword`, `Seed:EmployeeEmail`, `Seed:EmployeePassword` (o variables de entorno correspondientes).

## Frontend Angular

1. **`AuthService` (`core/services/auth.service.ts`):**
   - Mantiene el estado reactivo del usuario con `BehaviorSubject<User | null>`.
   - Almacena token (`gn_token`), usuario (`gn_user`) y fecha de vencimiento (`gn_expires_at`) en `localStorage`.
   - Limpia almacenamiento y notifica `null` al cerrar sesión (`logout()`).
   - Verifica expiración antes de devolver el token.

2. **Interceptor HTTP (`core/interceptors/auth.interceptor.ts`):**
   - Interceptor funcional registrado con `withInterceptors([authInterceptor])`.
   - Adjunta el encabezado `Authorization: Bearer <token>` a peticiones dirigidas al backend (`environment.apiBaseUrl`), excepto `/api/auth/login`.
   - Captura respuestas `401 Unauthorized` y desencadena `authService.logout()`.

3. **Guards de rutas:**
   - `authGuard`: Protege rutas privadas, redirigiendo a `/login?returnUrl=...`.
   - `roleGuard`: Restringe rutas por rol (`route.data['role']`), mejorando la experiencia de usuario.

4. **Pantalla de Login (`pages/login/login.component.ts`):**
   - Componente Standalone con Reactive Forms.
   - Validaciones en tiempo real para formato de email y campos requeridos.
   - Spinner de carga, prevención de envíos duplicados y botón de visibilidad de contraseña.
   - Mensajes amigables ante fallos de credenciales o errores de red.
