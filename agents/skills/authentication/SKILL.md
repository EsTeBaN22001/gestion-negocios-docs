# Skill — Authentication

## Leer antes

- `docs/08-authentication.md`
- `docs/02-business-rules.md`
- `docs/06-api.md`

## Reglas

- JWT.
- PasswordHasher.
- Roles Administrador/Empleado.
- `[Authorize]`.
- `[Authorize(Roles = "Administrador")]`.
- Backend como autoridad.

## Empleado

Nunca confiar en un `SucursalId` enviado por el cliente cuando la operación deba utilizar la sucursal del usuario.

Obtener identidad y sucursal desde claims/usuario autenticado.

## Angular

- interceptor para token;
- guards para navegación;
- manejar 401;
- no considerar ocultar botones como seguridad.

## Secretos

Nunca hardcodear JWT secret ni credenciales reales.
