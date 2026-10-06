# 24 — Fase 0: Infraestructura y arranque

## Objetivo

Dejar el workspace preparado para comenzar el desarrollo funcional sin que la primera tarea tenga que resolver decisiones de infraestructura.

La Fase 0 NO implementa módulos de negocio. Solo crea y verifica la base técnica.

## Resultado esperado

Al finalizar la Fase 0 debe existir:

```text
gestion-negocios/
├── AGENTS.md
├── README.md
├── docs/
├── agents/
├── backend/          # repositorio Git independiente
├── frontend/         # repositorio Git independiente
├── docker-compose.yml
├── .env.example
└── .gitignore
```

Y deben poder ejecutarse:

1. Backend ASP.NET Core .NET 8.
2. Frontend Angular.
3. MySQL mediante Docker Compose.
4. Backend conectado a MySQL mediante EF Core.
5. Swagger/OpenAPI.
6. Un endpoint de salud simple.
7. Angular comunicándose con el backend.
8. Migraciones de EF Core.

## Decisiones ya fijadas

- .NET 8.
- ASP.NET Core Web API.
- Entity Framework Core.
- MySQL.
- JWT se implementará en la fase de autenticación, no en Fase 0.
- Angular con Standalone Components.
- Bootstrap.
- Docker Compose.
- Dos repositorios GitHub: backend y frontend.
- Rama de trabajo: `develop`.
- Rama estable: `master`.

## Tareas de Fase 0

### P0-01 — Crear workspace

Crear la carpeta raíz y copiar la documentación de agentes.

### P0-02 — Crear repositorio backend

Crear `backend/` como repositorio Git independiente.

Base esperada:

```text
backend/
├── *.sln
├── src/
│   └── ...
├── tests/          # puede quedar preparado, sin suite extensa todavía
└── .gitignore
```

La estructura interna debe seguir la documentación de backend. No introducir proyectos adicionales sin necesidad.

### P0-03 — Crear API ASP.NET Core

Crear la Web API en .NET 8.

Debe compilar y ejecutar sin autenticación todavía.

Debe incluir Swagger/OpenAPI.

### P0-04 — Configurar EF Core + MySQL

Agregar los paquetes EF Core necesarios y el proveedor MySQL elegido.

Configurar `DbContext` y conexión mediante configuración/variables de entorno.

No poner contraseñas reales en Git.

### P0-05 — Crear esquema inicial

Incorporar las entidades ya definidas y sus relaciones.

Crear la primera migración EF Core.

Actualizar la base de datos de desarrollo y comprobar que las tablas se crean correctamente.

Todavía no implementar CRUD ni reglas completas de negocio.

### P0-06 — Crear Docker Compose

Servicios mínimos:

```text
mysql
backend
frontend
```

MySQL debe tener volumen persistente.

Backend y frontend deben poder comunicarse dentro de Compose.

Las imágenes deben construirse desde sus respectivos proyectos.

### P0-07 — Crear frontend Angular

Crear aplicación Angular con Standalone Components.

Configurar Bootstrap.

Crear una pantalla inicial mínima que permita comprobar que Angular está funcionando.

### P0-08 — Verificación de comunicación

Debe poder comprobarse:

```text
Angular → Backend → MySQL
```

Como mínimo:

- Angular carga.
- Backend responde.
- Swagger abre.
- Endpoint de salud responde.
- Backend puede consultar MySQL.
- Migraciones funcionan.

### P0-09 — Git y documentación

Configurar `develop` y `master` en ambos repositorios.

Realizar commits pequeños y descriptivos.

Actualizar:

- `docs/13-progress.md`
- `docs/17-environment.md`
- README de cada repositorio
- cualquier ADR si aparece una decisión nueva

## Orden obligatorio

```text
P0-01 Workspace
    ↓
P0-02 Repositorios
    ↓
P0-03 Backend base
    ↓
P0-04 EF Core + MySQL
    ↓
P0-05 Migración inicial
    ↓
P0-06 Docker Compose
    ↓
P0-07 Angular + Bootstrap
    ↓
P0-08 Integración y verificación
    ↓
P0-09 Git + documentación
```

## Qué NO hacer en Fase 0

No implementar todavía:

- login;
- JWT;
- roles;
- usuarios;
- sucursales;
- productos;
- categorías;
- stock;
- ventas;
- archivos;
- dashboards;
- paginación de negocio;
- búsquedas de negocio;
- lógica de descuentos de stock.

La única excepción es crear la estructura mínima necesaria para que esas funcionalidades puedan agregarse después.

## Criterio de salida

La Fase 0 está terminada únicamente cuando un desarrollador nuevo puede clonar los repositorios, seguir `docs/17-environment.md`, levantar la infraestructura y verificar el flujo base sin tener que tomar decisiones arquitectónicas nuevas.
