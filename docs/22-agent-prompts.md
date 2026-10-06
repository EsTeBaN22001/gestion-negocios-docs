# 22 — Agent Prompts

## Prompt general

Utilizar como prompt inicial cuando se abre una sesión de trabajo:

```text
Trabajá sobre el Sistema de Gestión de Negocios.

Antes de modificar código:
1. Lee AGENTS.md.
2. Lee docs/00-project-overview.md.
3. Lee docs/01-requirements.md.
4. Lee docs/02-business-rules.md.
5. Lee docs/03-architecture.md.
6. Lee la documentación específica de la tarea.
7. Lee las skills aplicables.

No inventes reglas ni arquitectura.
No agregues dependencias innecesarias.
No implementes patrones que el proyecto decidió no utilizar.
El backend es la autoridad de seguridad y negocio.

Primero analiza la tarea y dame un plan concreto.
No implementes todavía hasta que el plan esté claro.
```

---

## Prompt para backend

```text
Actuá como Backend Agent.

Leé:
- AGENTS.md
- docs/03-architecture.md
- docs/04-backend.md
- docs/05-database.md
- docs/06-api.md
- docs/02-business-rules.md
- agents/skills/backend/SKILL.md
- agents/skills/database/SKILL.md

Implementá únicamente la tarea indicada.

Respetá:
Controller → Service → DbContext.

Usá EF Core.
Usá DTOs.
No uses Repository Pattern.
No agregues arquitectura innecesaria.

Antes de terminar:
- compilá;
- verificá endpoints;
- revisá seguridad;
- actualizá documentación si corresponde.

Informá cambios y verificaciones.
```

---

## Prompt para frontend

```text
Actuá como Frontend Agent.

Leé:
- AGENTS.md
- docs/03-architecture.md
- docs/07-frontend.md
- docs/06-api.md
- docs/08-authentication.md
- agents/skills/frontend/SKILL.md

Usá:
- Standalone Components;
- Reactive Forms;
- Bootstrap;
- HttpClient;
- Services;
- Guards;
- Interceptor.

No uses NgRx.
No inventes endpoints.

Implementá únicamente la tarea indicada.

Antes de terminar:
- ejecutá build;
- verificá la pantalla;
- comprobá errores HTTP;
- informá cambios.
```

---

## Prompt para reviewer

```text
Actuá como Reviewer Agent.

No modifiques código.

Revisá el cambio actual contra:
- AGENTS.md
- docs/01-requirements.md
- docs/02-business-rules.md
- docs/03-architecture.md
- documentación específica.

Buscá:
- errores funcionales;
- problemas de seguridad;
- problemas de autorización;
- acceso incorrecto entre sucursales;
- problemas EF Core;
- errores de API;
- problemas Angular;
- incumplimientos académicos.

Clasificá cada hallazgo:
CRÍTICO / IMPORTANTE / MENOR.

Indicá archivo y ubicación cuando sea posible.
```

---

## Prompt para documentación

```text
Actuá como Documentation Agent.

Revisá los cambios realizados.

Actualizá solamente la documentación que realmente haya quedado desactualizada.

No inventes funcionalidades.

Revisá:
- docs/06-api.md
- docs/02-business-rules.md
- docs/05-database.md
- docs/15-university-compliance.md
- docs/13-progress.md

Informá exactamente qué documentación cambiaste.
```

---

# 5. Flujo recomendado de uso de prompts

No pedir:

```text
Hacé todo el módulo de ventas.
```

Preferir:

```text
Primero analizá el módulo de ventas y prepará el plan.
No implementes todavía.
```

Luego:

```text
Implementá solamente el backend de creación de ventas.
```

Luego:

```text
Probá y revisá el backend de ventas.
```

Luego:

```text
Implementá el frontend de creación de ventas usando el endpoint existente.
```

Luego:

```text
Revisá todo el flujo de ventas.
No modifiques código.
```

Finalmente:

```text
Actualizá la documentación y progress.
```
