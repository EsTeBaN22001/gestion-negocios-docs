# 00 — Project Overview

## Nombre

Sistema de Gestión de Negocios

## Objetivo

Desarrollar un sistema web para administrar un negocio que puede tener múltiples sucursales.

El sistema centraliza:

- usuarios y empleados;
- sucursales;
- categorías;
- productos;
- stock por sucursal;
- ventas;
- detalles de ventas.

## Idea principal del dominio

Los usuarios representan a las personas que utilizan el sistema. Un usuario con rol `Empleado` pertenece a una sucursal.

Los productos pertenecen a categorías.

El stock se separa de Producto porque un mismo producto puede existir en diferentes cantidades en distintas sucursales.

Una venta pertenece a una sucursal y al usuario que la realiza. Una venta tiene uno o más detalles, y cada detalle representa un producto vendido y su cantidad.

## Entidades

1. Usuario
2. Sucursal
3. Categoria
4. Producto
5. Stock
6. Venta
7. DetalleVenta

## Relaciones

```text
Sucursal 1 ─── N Usuario
Sucursal 1 ─── N Stock
Sucursal 1 ─── N Venta

Categoria 1 ─── N Producto

Producto 1 ─── N Stock
Producto 1 ─── N DetalleVenta

Usuario 1 ─── N Venta

Venta 1 ─── N DetalleVenta
```

## Roles

### Administrador

Puede administrar globalmente el sistema.

### Empleado

Opera dentro de su propia sucursal.

## Stack

```text
Frontend
Angular + TypeScript + Bootstrap

Backend
ASP.NET Core .NET 8 + C#

Persistencia
Entity Framework Core

Database
MySQL

Authentication
JWT

Infrastructure
Docker / Docker Compose
```

## Principios

El proyecto busca equilibrio entre:

- simplicidad;
- seguridad;
- claridad;
- cumplimiento académico;
- facilidad de mantenimiento;
- facilidad de trabajo con agentes de IA.

No se busca implementar una arquitectura empresarial innecesariamente compleja.
