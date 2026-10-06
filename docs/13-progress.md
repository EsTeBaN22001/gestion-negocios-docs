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
- [ ] Implementar autenticación
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
  - Repositorios Git independientes en backend y frontend con ramas 'main' y 'develop', y commits iniciales limpios.
Verificación:
  - Compilación de backend: dotnet build exitoso con 0 errores y 0 advertencias.
  - Migración EF Core: dotnet dotnet-ef migrations add InitialCreate completada exitosamente.
  - Compilación de frontend: npm run build de Angular completado con éxito (dist/gestion-negocios/browser).
Pendientes para Fase 1:
  - Autenticación JWT y módulo de usuarios (P1).
```

## Decisiones pendientes

Ninguna para infraestructura base. Todas las decisiones arquitectónicas de Fase 0 están alineadas con la documentación.
