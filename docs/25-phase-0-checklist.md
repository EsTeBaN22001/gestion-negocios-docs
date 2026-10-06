# 25 — Checklist de salida de Fase 0

Este checklist es obligatorio antes de comenzar la primera funcionalidad de negocio.

## Workspace

- [ ] Existe la carpeta raíz del workspace.
- [ ] `AGENTS.md` está en la raíz.
- [ ] `docs/` está completo.
- [ ] `agents/skills/` está disponible.
- [ ] Backend y frontend están separados.

## Git

- [ ] Backend tiene repositorio Git independiente.
- [ ] Frontend tiene repositorio Git independiente.
- [ ] Existe `main`.
- [ ] Existe `develop`.
- [ ] El trabajo actual se realiza en `develop`.
- [ ] `.gitignore` evita secretos, builds y dependencias.
- [ ] No hay contraseñas reales en Git.

## Backend

- [ ] .NET 8 está configurado.
- [ ] La solución compila.
- [ ] La API arranca.
- [ ] Swagger/OpenAPI funciona.
- [ ] Existe endpoint de salud.
- [ ] La configuración está separada por ambiente.
- [ ] EF Core está configurado.
- [ ] MySQL está configurado.
- [ ] `DbContext` arranca correctamente.
- [ ] La migración inicial fue creada.
- [ ] La migración puede aplicarse.

## Base de datos

- [ ] MySQL arranca.
- [ ] Existe volumen persistente.
- [ ] La base de desarrollo se crea.
- [ ] Las tablas iniciales se crean mediante migración.
- [ ] Las relaciones definidas coinciden con `docs/05-database.md`.
- [ ] No hay cambios de modelo sin documentar.

## Frontend

- [ ] Angular arranca.
- [ ] Se usa Standalone Components.
- [ ] Bootstrap está configurado.
- [ ] Existe pantalla inicial.
- [ ] El frontend conoce la URL de API mediante configuración.
- [ ] No hay URL de producción hardcodeada en componentes.

## Integración

- [ ] Angular puede comunicarse con la API.
- [ ] CORS funciona en desarrollo.
- [ ] API puede comunicarse con MySQL.
- [ ] Docker Compose levanta los servicios necesarios.
- [ ] El sistema puede ejecutarse localmente sin Docker según la documentación.

## Documentación

- [ ] `docs/17-environment.md` contiene comandos reales.
- [ ] README backend actualizado.
- [ ] README frontend actualizado.
- [ ] `docs/13-progress.md` actualizado.
- [ ] Nuevas decisiones registradas como ADR.

## Verificación final

Un agente nuevo debería poder ejecutar conceptualmente:

```text
clone
→ checkout develop
→ configurar .env
→ docker compose up --build
→ abrir Angular
→ abrir Swagger
→ comprobar health
→ comprobar conexión con MySQL
```

Si alguno de estos pasos requiere conocimiento que no está documentado, Fase 0 todavía no está cerrada.
