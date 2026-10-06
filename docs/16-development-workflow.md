# 16 — Development Workflow

## Flujo estándar

Para una funcionalidad nueva:

```text
1. Requisito
   ↓
2. Documentación
   ↓
3. Modelo/API
   ↓
4. Backend
   ↓
5. Frontend
   ↓
6. Pruebas
   ↓
7. Documentación
   ↓
8. Progress
```

## Ejemplo: CRUD de Producto

### Paso 1

Revisar:

- business rules;
- database;
- API;
- backend;
- frontend.

### Paso 2

Definir:

- DTOs;
- endpoints;
- validaciones;
- permisos.

### Paso 3

Implementar backend.

### Paso 4

Migración si la BD cambió.

### Paso 5

Implementar Angular:

- service;
- list;
- form;
- búsqueda;
- paginación.

### Paso 6

Probar.

### Paso 7

Actualizar documentación.

## Cambios de base de datos

No comenzar por el frontend si el contrato de datos todavía no está definido.

## Cambios de API

Cuando se cambie un endpoint:

1. actualizar backend;
2. revisar Swagger;
3. actualizar frontend;
4. actualizar documentación.

## Bug

Flujo:

```text
Reproducir
↓
identificar causa
↓
corregir
↓
probar
↓
documentar si corresponde
```

No aplicar un workaround sin entender el problema.
