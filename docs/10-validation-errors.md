# 10 — Validation and Errors

## Principio

Usar mecanismos estándar de ASP.NET Core siempre que sea posible.

No crear un sistema de errores excesivamente personalizado.

## Validación

La validación ocurre en capas:

### Frontend

Mejora la experiencia.

### Backend

Es obligatoria y constituye la autoridad.

## Tipos

### Validación de entrada

Ejemplos:

- campos obligatorios;
- longitud;
- email;
- números válidos;
- cantidades positivas.

Respuesta típica:

```text
400 Bad Request
```

## Autenticación

Sin credenciales/token válido:

```text
401 Unauthorized
```

## Autorización

Usuario autenticado pero sin permiso:

```text
403 Forbidden
```

## Recurso inexistente

```text
404 Not Found
```

## Conflictos

Ejemplos:

- código de producto duplicado;
- Producto + Sucursal duplicado;
- operación incompatible con estado actual.

```text
409 Conflict
```

## Errores de negocio

Ejemplo:

```text
No hay stock suficiente.
```

Debe devolverse mediante una respuesta HTTP apropiada, preferentemente `400` o `409` según la naturaleza concreta del conflicto.

## ProblemDetails

Preferir `ProblemDetails` de ASP.NET Core para errores de API.

No inventar estructuras distintas por Controller.

## Errores internos

No devolver stack traces ni información sensible al cliente en producción.

Registrar detalles internamente cuando exista logging.

## Frontend

Angular debe interpretar:

```text
400 → mostrar error de validación
401 → cerrar sesión/redirigir
403 → mostrar acceso denegado
404 → informar recurso inexistente
409 → informar conflicto
500 → mensaje genérico
```

No mostrar excepciones técnicas directamente al usuario.
