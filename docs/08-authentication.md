# 08 — Authentication

## Estrategia

Autenticación propia del proyecto utilizando:

- JWT;
- `PasswordHasher`;
- roles almacenados en Usuario.

No utilizar ASP.NET Core Identity inicialmente.

## Login

Flujo:

```text
Email + Password
        ↓
POST /api/auth/login
        ↓
buscar Usuario
        ↓
verificar PasswordHash
        ↓
comprobar Activo
        ↓
generar JWT
        ↓
devolver token + datos mínimos del usuario
```

## JWT

El JWT debe contener solamente claims necesarios, por ejemplo:

- identificador de usuario;
- email o username;
- rol;
- identificador de sucursal cuando corresponda.

No guardar información sensible dentro del token.

## Expiración

El token tendrá una expiración razonable definida en configuración.

No hardcodear secretos.

## Secretos

Nunca guardar en Git:

- JWT secret real;
- password real de MySQL;
- credenciales reales;
- API keys.

Usar:

- `appsettings.Development.json` solo para valores locales no sensibles si corresponde;
- variables de entorno;
- Docker secrets/configuración apropiada cuando corresponda.

## Autorización

Backend:

```csharp
[Authorize]
```

Rol:

```csharp
[Authorize(Roles = "Administrador")]
```

## Sucursal

Para Empleados, el backend obtiene la sucursal desde el usuario autenticado.

No confiar en:

```text
SucursalId enviado por Angular
```

cuando la operación deba utilizar la sucursal propia del empleado.

## PasswordHash

Nunca guardar password en texto plano.

Usar `PasswordHasher<TUser>` o mecanismo estándar equivalente disponible en ASP.NET Core.

## Usuario inactivo

Un usuario desactivado no debe poder iniciar sesión ni continuar accediendo a operaciones protegidas.

## Angular

Angular:

1. almacena el token según la estrategia definida;
2. agrega Authorization mediante interceptor;
3. utiliza guards para navegación;
4. reacciona a 401.

Esto no reemplaza la autorización del backend.
