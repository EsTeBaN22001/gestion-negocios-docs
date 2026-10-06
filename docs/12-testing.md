# 12 — Testing

## Objetivo

El testing no será el foco principal del proyecto.

Se busca una cobertura funcional razonable de los flujos críticos sin introducir una infraestructura de testing excesivamente compleja.

## Nivel esperado

### Durante desarrollo

- compilación;
- Swagger;
- pruebas manuales;
- pruebas con navegador;
- pruebas con Postman si se utiliza;
- revisión de respuestas HTTP.

### Antes de entrega

Comprobar al menos:

1. Login válido.
2. Login inválido.
3. Restricción por rol.
4. Restricción por sucursal.
5. CRUD de producto.
6. CRUD de categoría.
7. Consulta de stock.
8. Ajuste manual de stock.
9. Venta con stock suficiente.
10. Venta sin stock suficiente.
11. Descuento de stock.
12. Anulación de venta.
13. Restauración de stock.
14. Archivo adjunto.
15. Avatar.
16. Paginación.
17. Búsqueda server-side.

## Tests automatizados

Pueden agregarse algunos tests de backend para reglas críticas, especialmente:

- venta sin stock;
- descuento de stock;
- anulación/restauración;
- permisos.

No es obligatorio crear una suite enorme.

## Regla para agentes

No implementar testing complejo solo para aumentar cobertura numérica.

Priorizar pruebas de comportamiento crítico.
