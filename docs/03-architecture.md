# 03 — Architecture

## Objetivo

Mantener una arquitectura clásica, clara y fácil de entender.

No implementar patrones complejos sin una necesidad concreta.

## Arquitectura general

```text
Angular
   ↓
HTTP + JWT
   ↓
ASP.NET Core Web API
   ↓
Controllers
   ↓
Services
   ↓
ApplicationDbContext
   ↓
Entity Framework Core
   ↓
MySQL
```

## Backend

Estructura recomendada:

```text
backend/
├── Controllers/
├── Services/
├── Models/
├── DTOs/
├── Data/
├── Middleware/
├── Helpers/
├── Migrations/
├── wwwroot/
└── Program.cs
```

### Controllers

Responsabilidades:

- recibir HTTP requests;
- validar aspectos básicos de entrada;
- autorizar mediante atributos;
- llamar a Services;
- devolver respuestas HTTP.

Los Controllers no deben contener lógica de negocio compleja.

### Services

Responsabilidades:

- lógica de negocio;
- validaciones de negocio;
- consultas;
- operaciones transaccionales;
- coordinación entre entidades.

### Models

Representan entidades persistidas mediante EF Core.

### DTOs

Representan los datos de entrada/salida de la API.

No exponer entidades EF directamente como contrato general de la API.

### DbContext

`ApplicationDbContext` administra:

- DbSets;
- relaciones;
- configuraciones EF Core;
- acceso a la base.

## Repository Pattern

No se utilizará Repository Pattern.

La arquitectura será:

```text
Controller
    ↓
Service
    ↓
ApplicationDbContext
```

Motivo: el proyecto es de complejidad moderada y el patrón no es necesario para cumplir los objetivos.

## Mapping

El mapeo entre Entity y DTO será manual.

No utilizar AutoMapper ni otra librería de mapping salvo decisión posterior.

## Frontend

Angular utilizará:

- Standalone Components;
- Reactive Forms;
- HttpClient;
- Services;
- Router;
- Guards;
- HTTP Interceptor;
- Bootstrap.

## Estado

No se utilizará NgRx inicialmente.

El estado se manejará mediante servicios Angular y las herramientas nativas apropiadas.

## API

El backend será una API REST.

Angular no accede directamente a MySQL.

## Seguridad

El backend es la autoridad.

Angular puede ocultar elementos de UI, pero esto no reemplaza `[Authorize]` ni las validaciones de negocio.

## Docker

Docker se utilizará desde el inicio.

El objetivo es poder levantar:

- MySQL;
- backend;
- frontend;

mediante Docker Compose.

También debe ser posible ejecutar los proyectos localmente sin Docker, especialmente durante desarrollo.
