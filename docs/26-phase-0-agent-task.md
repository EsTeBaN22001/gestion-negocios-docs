# 26 — Tarea para el agente: ejecutar Fase 0

## Objetivo

Ejecutar completamente la Fase 0 del Sistema de Gestión de Negocios y dejar el workspace listo para comenzar el desarrollo funcional.

## Lectura obligatoria

Antes de modificar archivos, leer:

```text
AGENTS.md
docs/00-project-overview.md
docs/01-requirements.md
docs/02-business-rules.md
docs/03-architecture.md
docs/04-backend.md
docs/05-database.md
docs/07-frontend.md
docs/08-authentication.md
docs/14-git-workflow.md
docs/17-environment.md
docs/19-ai-development-workflow.md
docs/23-definition-of-done.md
docs/24-phase-0.md
docs/25-phase-0-checklist.md
agents/skills/project/SKILL.md
agents/skills/backend/SKILL.md
agents/skills/frontend/SKILL.md
agents/skills/database/SKILL.md
```

## Restricciones

- No implementar funcionalidades de negocio.
- No implementar JWT todavía.
- No usar ASP.NET Identity.
- No agregar Repository Pattern.
- No agregar CQRS, MediatR, Clean Architecture o NgRx.
- No agregar dependencias sin justificar su necesidad.
- No cambiar las entidades o relaciones documentadas sin detenerse y consultar.
- No poner secretos reales en archivos versionados.
- No marcar tareas como terminadas sin verificarlas.

## Plan esperado

1. Inspeccionar el entorno disponible.
2. Crear/validar workspace.
3. Crear backend .NET 8.
4. Crear frontend Angular.
5. Configurar EF Core + MySQL.
6. Crear entidades y migración inicial según documentación.
7. Configurar Docker Compose.
8. Configurar CORS y comunicación frontend/backend.
9. Crear endpoint de salud.
10. Ejecutar compilación, migraciones y pruebas manuales.
11. Actualizar documentación y progreso.
12. Realizar commits pequeños en `develop`.

## Antes de decidir algo no documentado

Detenerse y reportar:

```text
DECISIÓN REQUERIDA
Contexto:
Opciones:
Impacto:
Recomendación técnica (sin implementarla):
```

## Criterios de aceptación

La tarea solo se considera terminada si se cumplen todos los puntos de `docs/25-phase-0-checklist.md` que sean aplicables al entorno.

## Informe final obligatorio

El agente debe devolver:

```text
FASE 0 — RESULTADO

Estado: COMPLETADA / BLOQUEADA

Implementado:
- ...

Verificado:
- ...

Comandos probados:
- ...

Versiones detectadas:
- .NET:
- Node:
- Angular:
- EF Core:
- MySQL:
- Docker:

Commits realizados:
- ...

Documentación actualizada:
- ...

Problemas pendientes:
- ...

Decisiones que requieren al usuario:
- ...
```
