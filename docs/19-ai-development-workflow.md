# 19 — AI Development Workflow

## Objetivo

Este documento define el flujo oficial para desarrollar el proyecto utilizando agentes de IA.

La regla fundamental es:

> Los agentes implementan tareas pequeñas y verificables. Ningún agente debe intentar desarrollar todo el sistema de una sola vez.

---

## 1. Roles de los agentes

No es necesario utilizar agentes físicamente separados. Los roles representan responsabilidades distintas que una misma IA puede asumir.

### Project Agent

Responsable de:

- entender el contexto;
- dividir funcionalidades;
- controlar alcance;
- decidir qué documentación leer;
- coordinar el trabajo.

### Backend Agent

Responsable de:

- ASP.NET Core;
- Controllers;
- Services;
- DTOs;
- EF Core;
- JWT;
- API.

### Frontend Agent

Responsable de:

- Angular;
- componentes;
- formularios;
- servicios HTTP;
- guards;
- interceptor;
- Bootstrap.

### Database Agent

Responsable de:

- entidades;
- relaciones;
- migraciones;
- configuración EF Core;
- integridad de datos.

### Reviewer Agent

Responsable de:

- revisar código;
- buscar errores;
- comprobar seguridad;
- comprobar reglas de negocio;
- comprobar requisitos académicos.

### Documentation Agent

Responsable de:

- mantener documentación;
- actualizar progreso;
- registrar decisiones;
- mantener README y API alineados.

---

# 2. Flujo general

Cada funcionalidad debe seguir:

```text
REQUISITO
   ↓
ANÁLISIS
   ↓
PLAN
   ↓
IMPLEMENTACIÓN
   ↓
VERIFICACIÓN
   ↓
REVISIÓN
   ↓
DOCUMENTACIÓN
   ↓
COMMIT
```

No saltar directamente de requisito a código.

---

# 3. Paso 0 — Preparar el entorno

Antes de comenzar funcionalidades:

- crear repositorio backend;
- crear repositorio frontend;
- crear rama `develop`;
- configurar `.gitignore`;
- configurar Docker;
- configurar MySQL;
- crear proyecto ASP.NET;
- crear proyecto Angular;
- configurar Bootstrap;
- comprobar que backend y frontend arrancan;
- comprobar conexión backend → MySQL;
- comprobar frontend → backend;
- configurar Swagger;
- configurar configuración por entorno.

Resultado esperado:

```text
Docker funcionando
Backend funcionando
Frontend funcionando
MySQL funcionando
API accesible
Angular accesible
```

No comenzar CRUDs si esta base no funciona.

---

# 4. Paso 1 — Elegir una funcionalidad

Ejemplos:

```text
Login
CRUD Usuarios
CRUD Categorías
CRUD Productos
Stock
Ventas
Anulación de ventas
```

Una tarea debe representar una funcionalidad suficientemente pequeña para poder completarse y probarse.

### Correcto

```text
Implementar listado paginado de productos con búsqueda.
```

### Incorrecto

```text
Implementar todo el sistema.
```

---

# 5. Paso 2 — Análisis de impacto

Antes de programar, el agente debe identificar:

```text
¿Qué entidades intervienen?
¿Qué reglas de negocio intervienen?
¿Qué endpoints se necesitan?
¿Qué pantallas intervienen?
¿Qué permisos intervienen?
¿Hay cambios de base de datos?
¿Hay requisitos académicos relacionados?
```

Ejemplo:

```text
Funcionalidad:
Crear venta

Entidades:
Venta
DetalleVenta
Producto
Stock
Usuario
Sucursal

Reglas:
- usuario debe estar autenticado;
- empleado usa su sucursal;
- debe existir stock;
- no se puede vender más de lo disponible;
- venta necesita al menos un detalle;
- descontar stock;
- usar transacción.

Backend:
POST /api/ventas

Frontend:
Nueva venta
Selector de productos
Cantidad
Confirmación
```

---

# 6. Paso 3 — Revisar documentación

El agente debe leer únicamente la documentación necesaria para la tarea, además de `AGENTS.md`.

Por ejemplo, para ventas:

```text
AGENTS.md
docs/00-project-overview.md
docs/02-business-rules.md
docs/04-backend.md
docs/05-database.md
docs/06-api.md
docs/08-authentication.md
docs/11-pagination-search.md
```

Para frontend:

```text
AGENTS.md
docs/03-architecture.md
docs/07-frontend.md
docs/06-api.md
```

---

# 7. Paso 4 — Plan de implementación

Antes de modificar código, el agente debe producir un plan corto.

Ejemplo:

```text
Plan:

1. Crear VentaCreateDto.
2. Crear VentaResponseDto.
3. Implementar VentaService.
4. Validar usuario y sucursal.
5. Validar stock.
6. Crear Venta y DetalleVenta.
7. Descontar stock dentro de transacción.
8. Crear endpoint POST /api/ventas.
9. Probar con Swagger.
10. Implementar pantalla Angular.
11. Probar flujo completo.
```

Si el plan descubre una decisión no documentada, el agente debe preguntar.

---

# 8. Paso 5 — Implementar backend primero

Para funcionalidades que necesitan API, normalmente:

```text
Database
   ↓
Backend
   ↓
Frontend
```

### Motivo

Angular necesita conocer el contrato de la API.

---

# 9. Paso 6 — Cambios de base de datos

Si la funcionalidad requiere cambios de BD:

```text
Model
 ↓
EF Configuration
 ↓
Migration
 ↓
Database
```

Después:

- revisar la migración;
- ejecutarla;
- comprobar que la aplicación continúa arrancando.

Nunca asumir que cambiar una clase Entity cambia automáticamente una base existente.

---

# 10. Paso 7 — Implementar API

Implementar:

```text
DTO
Service
Controller
```

Ejemplo:

```text
VentaCreateDto
      ↓
VentaService
      ↓
VentasController
```

El Controller no debe contener la lógica de negocio de la venta.

---

# 11. Paso 8 — Probar backend aislado

Antes de crear la pantalla Angular:

- probar endpoint en Swagger;
- probar autenticación;
- probar permisos;
- probar errores;
- comprobar base de datos.

Para ventas:

```text
Venta correcta
Venta sin stock
Venta sin detalles
Empleado en otra sucursal
Venta anulada
Stock restaurado
```

---

# 12. Paso 9 — Implementar frontend

Una vez estable el endpoint:

```text
API
 ↓
Angular Service
 ↓
Component
 ↓
Template
```

Para una pantalla CRUD:

```text
List
Create
Edit
Delete
Search
Pagination
```

Según corresponda.

---

# 13. Paso 10 — Integración

Probar el flujo completo:

```text
Usuario
 ↓
Angular
 ↓
JWT
 ↓
API
 ↓
Service
 ↓
EF Core
 ↓
MySQL
```

No considerar una funcionalidad terminada solo porque backend y frontend compilan por separado.

---

# 14. Paso 11 — Revisión

Ejecutar un Reviewer Agent.

Debe revisar:

### Funcionalidad

- ¿Hace lo pedido?

### Seguridad

- ¿El backend realmente protege la operación?

### Sucursal

- ¿Empleado puede acceder solamente a su sucursal?

### Base

- ¿Las relaciones son correctas?

### Negocio

- ¿Se respetan las reglas?

### API

- ¿Los endpoints son coherentes?

### Frontend

- ¿No descarga datos innecesarios?

### Académico

- ¿Se cumple el requisito correspondiente?

---

# 15. Paso 12 — Documentación

Actualizar únicamente lo necesario.

Ejemplos:

```text
Cambio de API
→ docs/06-api.md

Cambio de regla
→ docs/02-business-rules.md

Cambio de arquitectura
→ docs/03-architecture.md
→ ADR correspondiente

Requisito terminado
→ docs/13-progress.md
→ docs/15-university-compliance.md
```

---

# 16. Paso 13 — Commit

Antes del commit:

```text
build OK
tests OK
flujo probado
sin secretos
documentación actualizada
```

Commit:

```text
feat: implementar crud de productos
```

---

# 17. Paso 14 — Actualizar progreso

Ejemplo:

```text
Fecha: 2026-10-01

Tarea:
CRUD de categorías.

Implementación:
- API completa.
- Angular completo.
- Búsqueda server-side.
- Paginación server-side.

Verificación:
- CRUD probado.
- Rol Administrador probado.
- Empleado recibe 403.

Pendientes:
- Ninguno.
```

---

# 18. Orden recomendado de desarrollo

El orden general recomendado es:

```text
1. Infraestructura
2. Base de datos
3. Configuración EF
4. Autenticación
5. Usuarios
6. Sucursales
7. Categorías
8. Productos
9. Stock
10. Ventas
11. Anulación
12. Archivos
13. Dashboard/consultas
14. Revisión
15. Testing final
16. Documentación de entrega
```

---

# 19. Dependencias entre funcionalidades

No desarrollar ventas antes de tener:

```text
Usuario
Sucursal
Producto
Stock
```

No desarrollar Stock antes de:

```text
Producto
Sucursal
```

No desarrollar Producto antes de:

```text
Categoria
```

Por eso el orden importa.

---

# 20. Regla de tamaño de tareas

Una tarea ideal debería poder describirse en:

```text
1 objetivo
3-10 pasos
1 resultado verificable
```

Si una tarea tiene demasiados objetivos, dividirla.

Ejemplo:

En vez de:

```text
Implementar productos.
```

usar:

```text
1. Crear entidad Producto.
2. Crear migración.
3. Crear endpoints CRUD.
4. Probar API.
5. Crear service Angular.
6. Crear listado.
7. Crear formulario.
8. Agregar búsqueda/paginación.
9. Probar flujo completo.
```

---

# 21. Cuando utilizar un agente de IA

La IA es especialmente útil para:

- implementar código repetitivo;
- crear DTOs;
- crear CRUD;
- crear formularios;
- generar consultas EF;
- crear componentes Angular;
- generar tests;
- revisar errores;
- revisar seguridad;
- actualizar documentación.

El desarrollador debe conservar el control sobre:

- decisiones de arquitectura;
- reglas de negocio;
- cambios de alcance;
- decisiones académicas.

---

# 22. Regla de continuidad

Cada agente debe poder continuar el trabajo de otro agente leyendo:

```text
AGENTS.md
docs/
agents/skills/
código existente
git history
```

No depender de que el agente anterior "recuerde" decisiones.

---

# 23. Definición de terminado

Una funcionalidad está terminada solamente cuando:

```text
[ ] Implementada
[ ] Compila
[ ] Funciona
[ ] Backend validado
[ ] Seguridad validada
[ ] Frontend integrado
[ ] Base de datos verificada
[ ] Reglas de negocio verificadas
[ ] Documentación actualizada
[ ] Progress actualizado
[ ] Sin errores conocidos
```
