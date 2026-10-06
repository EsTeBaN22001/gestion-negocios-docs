# 11 — Pagination and Search

## Objetivo

Cumplir el requisito de paginación y búsqueda server-side y mantener el sistema eficiente.

## Paginación

Las listas importantes deben recibir:

```text
page
pageSize
```

Ejemplo:

```http
GET /api/productos?page=2&pageSize=10
```

Backend:

```text
IQueryable
  ↓
Where
  ↓
OrderBy
  ↓
Count
  ↓
Skip
  ↓
Take
  ↓
ToListAsync
```

El orden exacto puede variar, pero nunca traer toda la colección innecesariamente.

## Respuesta

```json
{
  "items": [],
  "page": 2,
  "pageSize": 10,
  "totalItems": 100,
  "totalPages": 10
}
```

## PageSize

El backend debe imponer un máximo razonable para evitar peticiones abusivas.

Ejemplo conceptual:

```text
default = 10
max = 100
```

Los valores definitivos pueden ajustarse.

## Búsqueda

Ejemplo:

```http
GET /api/productos?search=coca&page=1&pageSize=10
```

La búsqueda se realiza en MySQL mediante EF Core.

## Entidades que deben soportar búsquedas

Como mínimo, las listas que tengan sentido operativo:

- Usuarios;
- Productos;
- Categorías;
- Sucursales;
- Stock;
- Ventas.

## Selección de relaciones

Cuando un formulario necesita seleccionar una entidad relacionada, usar búsqueda server-side.

Ejemplo:

```text
Nueva venta
 ↓
escribir "coca"
 ↓
GET /api/productos?search=coca...
 ↓
mostrar resultados
```

No cargar todos los productos al iniciar el formulario.

## Ordenamiento

Si se implementa ordenamiento dinámico:

- utilizar lista blanca de campos;
- no aceptar nombres de propiedades arbitrarios sin validación;
- tener ordenamiento predeterminado estable.

## Filtros por sucursal

El backend debe aplicar el filtro de sucursal según el usuario autenticado.

Nunca confiar en que Angular filtrará los datos correctamente.
