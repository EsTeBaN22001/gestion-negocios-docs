# 09 — File Management

## Objetivo

El sistema debe cumplir dos usos de archivos:

1. Avatar de Usuario.
2. Archivo adjunto opcional en Venta.

No se almacenarán imágenes de productos.

## Almacenamiento

Los archivos se almacenarán en el filesystem del backend.

Estructura conceptual:

```text
wwwroot/
└── uploads/
    ├── avatars/
    └── ventas/
```

La base de datos almacenará la referencia/ruta necesaria, no el contenido binario.

## Avatar

Usuario contiene una referencia al avatar.

Ejemplo conceptual:

```text
Avatar = "/uploads/avatars/..."
```

## Archivo de Venta

Venta contiene:

```text
ArchivoAdjunto
```

El archivo es opcional.

Ejemplos:

- comprobante;
- factura;
- ticket;
- documento relacionado con la operación.

No se implementará generación automática de documentos salvo que se solicite posteriormente.

## Seguridad

El backend debe:

- validar tamaño máximo;
- validar extensión;
- validar MIME type cuando corresponda;
- generar nombres de archivo seguros;
- evitar confiar en el nombre original;
- evitar path traversal;
- no ejecutar archivos subidos;
- impedir rutas arbitrarias.

## Nombre físico

Preferir nombres generados por el sistema, por ejemplo GUID, en lugar de utilizar directamente el nombre original.

## Eliminación

Si se reemplaza un archivo, evaluar si el archivo anterior debe eliminarse.

No borrar archivos de forma irreversible sin comprobar que no sean utilizados por otro registro.

## Docker

Los uploads deben contemplar persistencia mediante volumen cuando el sistema se ejecute en Docker.

El archivo subido no debe desaparecer simplemente porque se recreó el contenedor.

## Límites

Definir límites razonables de tamaño y tipos permitidos en configuración.

No aceptar archivos ilimitados.
