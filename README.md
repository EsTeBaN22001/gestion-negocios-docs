# Sistema de Gestión de Negocios

Sistema web para administrar un negocio con múltiples sucursales.

## Tecnologías

### Backend

- ASP.NET Core .NET 8
- C#
- Entity Framework Core
- MySQL
- JWT
- REST API
- Swagger/OpenAPI

### Frontend

- Angular
- TypeScript
- Standalone Components
- Reactive Forms
- Bootstrap

### Infraestructura

- Docker
- Docker Compose

La versión exacta de Angular y las versiones exactas de paquetes deben quedar registradas en el proyecto cuando se cree.

## Repositorios

El backend y frontend se mantienen como repositorios GitHub independientes:

```text
backend → repositorio GitHub del backend
frontend → repositorio GitHub del frontend
```

La carpeta superior sirve como workspace común.

## Estructura del workspace

```text
gestion-negocios/
├── AGENTS.md
├── README.md
├── docs/
├── agents/
├── backend/
└── frontend/
```

## Funcionalidades principales

- Login con JWT.
- Roles Administrador y Empleado.
- Gestión de usuarios.
- Gestión de sucursales.
- Gestión de categorías.
- Gestión de productos.
- Gestión de stock por sucursal.
- Ajuste manual de stock por administrador.
- Registro de ventas.
- Detalle de ventas.
- Descuento automático de stock.
- Anulación de ventas y devolución de stock.
- Avatar de usuario.
- Archivo adjunto opcional en ventas.
- Paginación server-side.
- Búsquedas server-side.
- Selección de entidades relacionadas mediante búsqueda AJAX/HTTP.
- Filtrado por sucursal según usuario autenticado.

## Desarrollo

El proyecto está pensado para poder ejecutarse:

1. Con Docker Compose.
2. Localmente sin Docker, si se desea.

Durante desarrollo se espera aproximadamente:

```text
Angular   → http://localhost:4200
ASP.NET   → puerto configurado por el proyecto
MySQL     → localhost:3306
```

Los puertos definitivos se documentarán cuando se cree la configuración.

## Documentación para agentes

Antes de trabajar, leer:

```text
AGENTS.md
docs/00-project-overview.md
docs/01-requirements.md
docs/02-business-rules.md
docs/03-architecture.md
```

y luego la documentación específica del área.

## Estado

Consultar `docs/13-progress.md`.

La Fase 0 de infraestructura está especificada en `docs/24-phase-0.md` y su checklist de salida en `docs/25-phase-0-checklist.md`. La tarea lista para entregar a un agente está en `docs/26-phase-0-agent-task.md`.

## Git

Ramas principales:

```text
main
develop
```

El desarrollo se realiza en `develop`.

`main` representa una versión estable/producción.

Convención de commits:

```text
feat:
fix:
refactor:
docs:
test:
chore:
```
