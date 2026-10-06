# 25 — Checklist de salida de Fase 0

Este checklist es obligatorio antes de comenzar la primera funcionalidad de negocio.

## Workspace

- [x] Existe la carpeta raíz del workspace.
- [x] `AGENTS.md` está en la raíz.
- [x] `docs/` está completo.
- [x] `agents/skills/` está disponible.
- [x] Backend y frontend están separados.

## Git

- [x] Backend tiene repositorio Git independiente.
- [x] Frontend tiene repositorio Git independiente.
- [x] Existe `main`.
- [x] Existe `develop`.
- [x] El trabajo actual se realiza en `develop`.
- [x] `.gitignore` evita secretos, builds y dependencias.
- [x] No hay contraseñas reales en Git.

## Backend

- [x] .NET 8 está configurado.
- [x] La solución compila.
- [x] La API arranca.
- [x] Swagger/OpenAPI funciona.
- [x] Existe endpoint de salud.
- [x] La configuración está separada por ambiente.
- [x] EF Core está configurado.
- [x] MySQL está configurado.
- [x] `DbContext` arranca correctamente.
- [x] La migración inicial fue creada.
- [x] La migración puede aplicarse.

## Base de datos

- [x] MySQL arranca (vía Docker Compose con mysql:8.0).
- [x] Existe volumen persistente.
- [x] La base de desarrollo se crea.
- [x] Las tablas iniciales se crean mediante migración.
- [x] Las relaciones definidas coinciden con `docs/05-database.md`.
- [x] No hay cambios de modelo sin documentar.

## Frontend

- [x] Angular arranca.
- [x] Se usa Standalone Components.
- [x] Bootstrap está configurado.
- [x] Existe pantalla inicial.
- [x] El frontend conoce la URL de API mediante configuración.
- [x] No hay URL de producción hardcodeada en componentes.

## Integración

- [x] Angular puede comunicarse con la API (ApiService configurado).
- [x] CORS funciona en desarrollo (política DevelopmentPolicy en Program.cs).
- [x] API puede comunicarse con MySQL (EF Core con retry policy y health check).
- [x] Docker Compose levanta los servicios necesarios (mysql, backend, frontend).
- [x] El sistema puede ejecutarse localmente sin Docker según la documentación.

## Documentación

- [x] `docs/17-environment.md` contiene comandos reales.
- [x] README backend actualizado.
- [x] README frontend actualizado.
- [x] `docs/13-progress.md` actualizado.
- [x] Nuevas decisiones registradas como ADR (sin discrepancias con la arquitectura definida).

## Verificación final

Un desarrollador nuevo puede ejecutar conceptualmente:

```text
clone
→ checkout develop
→ configurar .env
→ docker compose up --build
→ abrir Angular (http://localhost:4200)
→ abrir Swagger (http://localhost:5000/swagger)
→ comprobar health (/api/health)
→ comprobar conexión con MySQL (/api/health/db)
```

Fase 0 cerrada y lista para comenzar las fases de negocio.
