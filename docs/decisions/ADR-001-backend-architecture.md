# ADR-001 — Arquitectura simple del backend

## Estado

Aceptado.

## Decisión

El backend utilizará:

```text
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

## Motivo

El proyecto necesita una separación clara de responsabilidades, pero no requiere Clean Architecture ni una arquitectura empresarial.

La estructura es fácil de aprender, implementar y explicar.

## Consecuencia

Los agentes no deben crear capas adicionales sin una necesidad documentada.
