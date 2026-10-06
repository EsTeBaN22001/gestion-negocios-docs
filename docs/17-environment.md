# 17 — Environment and Docker

## Objetivo

Docker debe utilizarse desde el inicio, pero el proyecto debe seguir pudiendo ejecutarse localmente.

## Servicios

Conceptualmente:

```text
frontend
backend
mysql
```

## Docker Compose

El `docker-compose.yml` debe permitir levantar el entorno completo.

## MySQL

MySQL debe utilizar un volumen persistente.

No depender de que los datos sobrevivan sin volumen.

## Backend

El backend debe recibir configuración mediante variables de entorno/configuración.

La cadena de conexión no debe contener secretos reales en el repositorio.

## Frontend

El frontend debe poder conocer la URL de API mediante configuración de entorno apropiada.

No hardcodear URLs de producción dentro de componentes.

## Ejecución local sin Docker

Debe ser posible:

```text
MySQL local
+
dotnet run
+
ng serve
```

## Desarrollo

La documentación definitiva debe registrar:

- puertos;
- nombres de servicios;
- variables necesarias;
- comandos;
- credenciales de desarrollo.

No registrar secretos reales.

## Producción

`main` representa la versión estable.

La configuración de producción debe estar separada de la configuración local.
