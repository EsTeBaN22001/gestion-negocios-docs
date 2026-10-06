# 07 — Frontend

## Tecnología

- Angular.
- TypeScript.
- Standalone Components.
- Reactive Forms.
- HttpClient.
- Router.
- Guards.
- HTTP Interceptor.
- Bootstrap.

La versión de Angular será la versión estable recomendada al momento de iniciar el proyecto y se registrará en el proyecto.

## Arquitectura

```text
src/app/
├── core/
├── shared/
└── pages/
```

## Core

Contendrá funcionalidades globales:

```text
auth
guards
interceptors
services
```

## Shared

Contendrá componentes, modelos o utilidades reutilizables.

No colocar aquí lógica específica de una pantalla.

## Pages

Organizar por funcionalidad:

```text
login
dashboard
usuarios
sucursales
categorias
productos
stock
ventas
```

## Standalone Components

Utilizar Standalone Components.

No crear NgModules innecesarios.

## Reactive Forms

Los formularios del proyecto utilizarán Reactive Forms.

La validación del frontend sirve para mejorar UX.

El backend debe validar nuevamente.

## HTTP

Los componentes no deberían contener llamadas HTTP complejas directamente.

Preferir:

```text
Component
   ↓
Service
   ↓
HttpClient
   ↓
API
```

## JWT

El token será agregado automáticamente mediante un HTTP Interceptor.

No duplicar manualmente:

```text
Authorization: Bearer ...
```

en cada servicio.

## Guards

Los guards se utilizan para experiencia/navegación.

La seguridad real continúa en el backend.

## Bootstrap

Utilizar Bootstrap para:

- layout;
- formularios;
- botones;
- tablas;
- modales;
- alertas;
- navegación;
- responsive.

Evitar CSS personalizado cuando Bootstrap resuelva correctamente el problema.

## Búsqueda

Los campos de búsqueda deben consultar la API.

No descargar colecciones completas para filtrar en memoria.

## Paginación

Angular consume la paginación del backend.

El frontend no debe implementar paginación sobre una lista completa descargada.

## Manejo de sesión

Angular debe poder:

- detectar token;
- mantener sesión;
- enviar token;
- detectar 401;
- cerrar sesión;
- redirigir a login.

## Rol

El frontend puede adaptar la interfaz al rol:

```text
Administrador → opciones administrativas
Empleado → opciones operativas
```

Pero el backend siempre debe verificar permisos.
