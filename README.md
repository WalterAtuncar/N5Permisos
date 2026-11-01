# N5Permisos — API de gestión de permisos (.NET + CQRS)

API REST para solicitar, modificar y consultar permisos de empleados, desarrollada como reto técnico. Demuestra una arquitectura por capas con CQRS, persistencia en SQL Server, indexación en Elasticsearch y publicación de eventos en Kafka.

## Stack

* ASP.NET Core Web API (C#)
* CQRS con commands, queries y handlers
* Entity Framework Core + SQL Server (migraciones)
* Repository + Unit of Work
* Elasticsearch (indexación de permisos)
* Kafka (registro de eventos por operación)
* xUnit (pruebas del controlador)
* Docker

## Estructura

| Proyecto | Responsabilidad |
|---|---|
| `N5PermisosAPI` | Controladores y configuración de la API |
| `CQRS` | Commands (`SolicitarPermiso`, `ModificarPermiso`, `CrearTipoPermiso`), queries y handlers |
| `DataAccess` | Repositorios, Unit of Work y publicación de eventos |
| `Data` | DbContext, entidades, migraciones y settings |
| `N5PermisosAPI.Tests` | Pruebas unitarias |

## Endpoints

* **Solicitar permiso**: crea un permiso, lo indexa en Elasticsearch y publica el evento en Kafka.
* **Modificar permiso**: actualiza un permiso existente.
* **Obtener permisos**: lista los permisos registrados.

## Cómo ejecutarlo

1. Crea `N5PermisosAPI/appsettings.json` con tu configuración local:

```json
{
  "ConnectionStrings": {
    "N5PermisosAPIContext": "Server=localhost;Database=N5-Challenge;User Id=YOUR_USER;Password=YOUR_PASSWORD;TrustServerCertificate=True;"
  },
  "Elasticsearch": { "Uri": "http://localhost:9200" },
  "Kafka": { "BootstrapServers": "localhost:9092" },
  "AllowedHosts": "*"
}
```

2. Aplica las migraciones: `dotnet ef database update --project Data --startup-project N5PermisosAPI`
3. Ejecuta la API: `dotnet run --project N5PermisosAPI`
4. Pruebas: `dotnet test`

### Docker

```bash
docker build -t n5dockerapi -f Dockerfile .
```

## Autor

Walter Atúncar Céspedes — Full Stack Senior .NET / Angular / React · Lima, Perú
