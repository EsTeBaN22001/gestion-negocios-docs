# 18 — Agent Protocol

## Objetivo

Definir cómo debe comportarse un agente de IA durante el desarrollo.

## Fase 1 — Contexto

Leer documentación antes de modificar.

## Fase 2 — Comprensión

Identificar:

- objetivo;
- archivos afectados;
- entidades;
- endpoints;
- reglas;
- permisos;
- impacto académico.

## Fase 3 — Plan

Crear internamente un plan corto.

Si la tarea es ambigua o requiere una decisión arquitectónica, preguntar.

## Fase 4 — Implementación

Implementar el cambio mínimo necesario.

No refactorizar todo el proyecto sin necesidad.

## Fase 5 — Verificación

Ejecutar:

- build;
- tests disponibles;
- pruebas funcionales;
- migraciones si corresponden.

## Fase 6 — Documentación

Actualizar únicamente lo que cambió.

## Fase 7 — Progress

Actualizar `docs/13-progress.md`.

## Fase 8 — Informe

Al finalizar, informar:

```text
Implementado:
- ...

Verificado:
- ...

Documentación:
- ...

Pendientes:
- ...
```

## Regla de no invención

Si falta información importante:

```text
NO SUPONER
```

Preguntar.

## Regla de compatibilidad

Antes de cambiar una API, entidad o contrato utilizado por otra aplicación, comprobar dependencias.

## Regla de mínimo cambio

Modificar solamente lo necesario para resolver la tarea.

## Regla de seguridad

Si una solución depende de confiar en el frontend para proteger información, es incorrecta.

## Regla de dominio

Las reglas de negocio deben vivir en backend.

## Regla académica

Una solución técnicamente correcta pero que elimine un requisito de la materia no es aceptable.

## Regla final

No declarar una tarea terminada si:

- no compila;
- tiene errores conocidos;
- rompe una regla;
- no fue verificada;
- o requiere una decisión que nunca fue aprobada.
