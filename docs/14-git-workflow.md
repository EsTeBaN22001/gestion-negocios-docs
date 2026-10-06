# 14 — Git Workflow

## Repositorios

Existen dos repositorios GitHub independientes:

```text
backend
frontend
```

## Ramas

Cada repositorio tendrá:

```text
main
develop
```

### main

Representa una versión estable/producción.

### develop

Rama principal de desarrollo.

El trabajo habitual se realiza sobre `develop`.

## Feature branches

No es obligatorio crear una rama para cada pequeño cambio.

Cuando sea útil, pueden utilizarse:

```text
feature/auth
feature/productos
feature/ventas
fix/stock
```

## Commits

Usar Conventional Commits simplificados:

```text
feat:
fix:
refactor:
docs:
test:
chore:
```

Ejemplos:

```text
feat: implementar login con jwt
feat: agregar crud de productos
fix: corregir descuento de stock
docs: actualizar reglas de ventas
test: validar anulación de ventas
chore: configurar docker
```

## Commits de IA

Un agente puede realizar commits solo si el usuario le permite hacerlo.

Antes del commit:

- compilar;
- ejecutar pruebas disponibles;
- revisar cambios;
- verificar que no haya secretos.

## Pull Requests

Si se utilizan PRs:

```text
feature → develop
develop → main
```

## No hacer

- No subir secrets.
- No subir passwords.
- No subir `.env` con credenciales reales.
- No hacer force push sobre `main` sin autorización.
- No reescribir historial compartido sin autorización.
