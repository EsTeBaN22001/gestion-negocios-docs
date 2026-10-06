# ADR-002 — No Repository Pattern

## Estado

Aceptado.

## Decisión

No utilizar Repository Pattern.

Los Services accederán a `ApplicationDbContext`.

## Motivo

EF Core ya proporciona una abstracción de persistencia adecuada para este proyecto.

Agregar repositories generaría código adicional sin una necesidad concreta.

## Consecuencia

No crear automáticamente:

```text
IProductoRepository
ProductoRepository
IVentaRepository
VentaRepository
```

Si en el futuro aparece una necesidad real, debe discutirse y documentarse antes.
