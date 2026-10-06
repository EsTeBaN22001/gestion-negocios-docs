# ADR-003 — JWT

## Estado

Aceptado.

## Decisión

La autenticación utilizará JWT.

## Motivo

El frontend Angular consume una API REST y JWT permite transportar la identidad y autorización de forma adecuada para este escenario.

## Consecuencia

Los endpoints protegidos deben utilizar autenticación JWT.

Angular utilizará un interceptor para agregar el token.
