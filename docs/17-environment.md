# 17 — Environment and Docker

## Objetivo

Docker se utiliza para orquestar la infraestructura, garantizando reproducibilidad, y el proyecto también puede ejecutarse de manera local nativa.

## Servicios en Docker Compose

| Servicio   | Contenedor                  | Puerto Host | Puerto Contenedor | Descripción                       |
|------------|-----------------------------|-------------|-------------------|-----------------------------------|
| `mysql`    | `gestion-negocios-mysql`    | 3306        | 3306              | Base de datos MySQL 8.0           |
| `backend`  | `gestion-negocios-backend`  | 5000        | 8080              | ASP.NET Core 8 Web API            |
| `frontend` | `gestion-negocios-frontend` | 4200        | 80                | Angular 18 servido por Nginx      |

## Persistencia

- MySQL utiliza un volumen nombrado `mysql_data` persistido en el host.
- Incluye healthcheck con `mysqladmin ping` para asegurar que el backend inicie cuando MySQL esté listo.

## Variables de Entorno (`.env`)

Copia `.env.example` a `.env` en la raíz del workspace antes de iniciar:

```bash
cp .env.example .env
```

Variables disponibles:
- `MYSQL_DATABASE`: Nombre de la base de datos (por defecto: `gestion_negocios`)
- `MYSQL_USER`: Usuario de la base de datos (por defecto: `appuser`)
- `MYSQL_PASSWORD`: Contraseña del usuario
- `MYSQL_ROOT_PASSWORD`: Contraseña de root
- `ASPNETCORE_ENVIRONMENT`: Ambiente de ASP.NET Core (`Development` o `Production`)

## Comandos con Docker Compose

1. **Iniciar todo el entorno:**
   ```bash
   docker compose up --build
   ```

2. **Iniciar en segundo plano:**
   ```bash
   docker compose up -d
   ```

3. **Ver logs:**
   ```bash
   docker compose logs -f
   ```

4. **Detener servicios:**
   ```bash
   docker compose down
   ```

5. **Detener y eliminar volúmenes (reset de datos):**
   ```bash
   docker compose down -v
   ```

## Ejecución Local sin Docker

### 1. Iniciar MySQL
Asegúrate de tener un servicio MySQL local activo en el puerto 3306 (por ejemplo vía Laragon, XAMPP o Docker solo para la BD):
```bash
docker compose up -d mysql
```

### 2. Ejecutar Backend
```bash
cd backend
dotnet run --project src/GestionNegocios.Api
```
- Swagger UI disponible en: [http://localhost:5000/swagger](http://localhost:5000/swagger)
- Endpoint de verificación: [http://localhost:5000/api/health](http://localhost:5000/api/health)
- Endpoint de conexión a BD: [http://localhost:5000/api/health/db](http://localhost:5000/api/health/db)

### 3. Ejecutar Frontend
```bash
cd frontend
npm install
npm start
```
- Aplicación Angular disponible en: [http://localhost:4200](http://localhost:4200)

## Migraciones de Base de Datos

Las migraciones de EF Core se aplican automáticamente al arrancar la API si la base de datos está disponible. Para administrarlas manualmente desde la terminal:

```bash
cd backend
# Crear una nueva migración
dotnet dotnet-ef migrations add <NombreMigracion> --project src/GestionNegocios.Api

# Aplicar migraciones a la BD
dotnet dotnet-ef database update --project src/GestionNegocios.Api
```
