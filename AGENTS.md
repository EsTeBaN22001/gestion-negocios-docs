# AGENTS.md — Sistema de Gestión de Negocios

## 1. Propósito

Este archivo es la instrucción principal para cualquier agente de IA que trabaje en el proyecto.

El proyecto consiste en un sistema web para administrar un negocio con múltiples sucursales, usuarios/empleados, productos, categorías, stock y ventas.

El proyecto tiene dos aplicaciones independientes:

- `backend/`: ASP.NET Core Web API con C#.
- `frontend/`: Angular.

Ambos proyectos tendrán repositorios GitHub independientes. La carpeta raíz funciona como workspace común y contiene documentación compartida para los agentes.

## 2. Regla principal

Antes de modificar código, el agente DEBE:

1. Leer este archivo.
2. Leer `docs/00-project-overview.md`.
3. Leer `docs/01-requirements.md`.
4. Leer `docs/02-business-rules.md`.
5. Leer `docs/03-architecture.md`.
6. Leer la documentación específica de la parte que va a modificar.
7. Leer las skills aplicables de `agents/skills/`.

Si existe una contradicción entre documentación y código, el agente debe detenerse, informar la contradicción y solicitar una decisión. No debe inventar una solución arquitectónica.

## 3. Principios obligatorios

- Mantener la solución simple.
- No introducir complejidad arquitectónica sin necesidad.
- No agregar librerías, patrones o tecnologías porque "son más profesionales" si no existe una necesidad concreta.
- No cambiar reglas de negocio sin autorización.
- No cambiar relaciones de base de datos sin revisar `docs/05-database.md`.
- No confiar en Angular para seguridad.
- Toda autorización real debe existir en el backend.
- No cargar colecciones completas para paginar o buscar en el frontend.
- Las búsquedas y paginaciones deben ejecutarse en el servidor.
- Usar DTOs para las entradas/salidas de la API.
- Los mapeos entre entidades y DTOs serán manuales.
- No utilizar Repository Pattern.
- No utilizar CQRS, MediatR, Clean Architecture, NgRx u otros patrones complejos salvo decisión explícita.
- Usar Entity Framework Core como acceso a datos.
- Usar migraciones de EF Core para administrar el esquema.
- Usar JWT para autenticación.
- Usar `PasswordHasher` para almacenar/verificar contraseñas.
- Usar Bootstrap en Angular.
- Usar Standalone Components.
- Usar Reactive Forms.
- Mantener el backend como autoridad de seguridad y reglas de negocio.

## 4. Flujo de trabajo de un agente

### Antes de implementar

1. Identificar el requisito.
2. Identificar las entidades afectadas.
3. Revisar las reglas de negocio.
4. Revisar endpoints existentes.
5. Revisar código existente para evitar duplicación.
6. Determinar qué documentación deberá actualizarse.
7. Si el cambio requiere una decisión no documentada, preguntar antes de implementarlo.

### Durante la implementación

- Hacer cambios pequeños y coherentes.
- Seguir la estructura existente.
- Reutilizar servicios/componentes existentes cuando corresponda.
- No duplicar lógica de negocio.
- Validar entradas en backend.
- Mantener respuestas HTTP y errores consistentes.
- No modificar archivos no relacionados sin motivo.

### Después de implementar

1. Compilar.
2. Ejecutar las pruebas disponibles.
3. Probar el flujo funcional relevante.
4. Revisar errores de autorización.
5. Actualizar documentación si cambió comportamiento, API, BD o requisitos.
6. Actualizar `docs/13-progress.md`.
7. Informar claramente qué se modificó, qué se verificó y qué queda pendiente.

## 5. Cuándo preguntar al usuario

El agente puede trabajar autónomamente en cambios rutinarios.

DEBE pedir autorización antes de:

- Cambiar arquitectura.
- Agregar una dependencia importante.
- Agregar una nueva tecnología.
- Crear/eliminar una entidad.
- Cambiar relaciones entre entidades.
- Cambiar reglas de negocio.
- Cambiar autenticación o autorización.
- Cambiar el contrato público de una API existente de forma incompatible.
- Eliminar datos o migraciones existentes.
- Introducir un patrón arquitectónico no documentado.
- Resolver una contradicción entre documentación y código.

## 6. Fase 0

Antes de comenzar cualquier funcionalidad de negocio, el proyecto debe completar `docs/24-phase-0.md` y satisfacer `docs/25-phase-0-checklist.md`. Si la Fase 0 no está cerrada, el agente debe trabajar en infraestructura o reportar el bloqueo; no debe saltar directamente a módulos de negocio.

## 7. Estructura documental

- `docs/00-project-overview.md`: visión general.
- `docs/01-requirements.md`: requisitos funcionales y técnicos.
- `docs/02-business-rules.md`: reglas de negocio.
- `docs/03-architecture.md`: arquitectura.
- `docs/04-backend.md`: reglas del backend.
- `docs/05-database.md`: entidades, relaciones y EF Core.
- `docs/06-api.md`: contrato y convenciones de API.
- `docs/07-frontend.md`: Angular.
- `docs/08-authentication.md`: JWT, roles y seguridad.
- `docs/09-file-management.md`: avatares y archivos adjuntos.
- `docs/10-validation-errors.md`: validaciones y errores.
- `docs/11-pagination-search.md`: paginación y búsquedas.
- `docs/12-testing.md`: estrategia de pruebas.
- `docs/13-progress.md`: estado del proyecto.
- `docs/14-git-workflow.md`: Git.
- `docs/15-university-compliance.md`: requisitos de la materia.
- `docs/decisions/`: decisiones arquitectónicas.

## 8. Skills

Las skills están en:

`agents/skills/`

Skills iniciales:

- `project`
- `backend`
- `frontend`
- `database`
- `authentication`
- `testing`
- `documentation`
- `reviewer`

Las skills complementan la documentación; no reemplazan las reglas del proyecto.

## 9. Principio de mínima complejidad

Ante dos soluciones correctas, elegir la que:

1. Sea más simple.
2. Sea más fácil de explicar.
3. Tenga menos dependencias.
4. Sea más fácil de probar.
5. Sea más fácil de mantener por un estudiante.
6. Cumpla igualmente los requisitos académicos.

No optimizar prematuramente.

## 10. Fuente de verdad

La documentación del proyecto describe las decisiones intencionales.

El código representa la implementación.

Si ambos están en conflicto, el agente no debe asumir cuál tiene razón: debe informar la diferencia.
