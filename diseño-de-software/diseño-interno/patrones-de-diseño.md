# Patrones de diseño

## Objetivo

Documentar los patrones de diseño aplicados en el backend del Sistema de Gestión Escalafonaria del Personal Municipal, indicando dónde se utilizan, qué problema resuelven y con qué mecanismos se implementan, para mantener una estructura uniforme y desacoplada.

## Contexto

- **Estilo:** monolito modular sobre ASP.NET Core / .NET 8.
- **Enfoque interno:** Clean Architecture.
- **Persistencia principal:** PostgreSQL mediante Entity Framework Core y Npgsql.
- **Caché:** Redis como optimización opcional.
- **Base:** arquitectura por capas y módulos funcionales M01–M10. fileciteturn298file9

## Patrones aplicados

| Patrón | Dónde se usa | Problema que resuelve | Se implementa con | Archivos / elementos representativos |
|---|---|---|---|---|
| **Repository** | Módulos funcionales → PostgreSQL | Las reglas del negocio no deben conocer Entity Framework Core, SQL ni detalles de persistencia. | Interfaces en Application e implementaciones en Infrastructure con EF Core. | `ITrabajadorRepository`, `ILegajoRepository`, `TrabajadorRepository`, `LegajoRepository` |
| **Adapter** | M10 Integraciones → RENIEC y servicio de validación tributaria | Los servicios externos poseen contratos propios y pueden cambiar o no estar disponibles. | Interfaces de aplicación y adaptadores concretos en Infrastructure. | Servicio de validación de identidad, adaptador RENIEC, adaptador de validación tributaria |
| **Dependency Injection** | Composición de API, casos de uso y repositorios | Evita que los casos de uso creen directamente implementaciones concretas y reduce el acoplamiento. | Contenedor DI nativo de ASP.NET Core mediante `Program.cs` y `IServiceCollection`. | `Program.cs`, registro de `ITrabajadorRepository → TrabajadorRepository` |
| **Cache-Aside** | Sesiones, permisos y consultas repetitivas cuando sea necesario | Reduce consultas repetitivas sin convertir a Redis en fuente de verdad. | PostgreSQL como fuente principal y Redis como caché opcional. | Servicios de caché en Infrastructure, consultas de permisos/sesiones/dashboard cacheables |

El diseño aprobado mantiene los repositorios como abstracciones para persistencia, integraciones externas desacopladas y Redis únicamente como mecanismo opcional de optimización; PostgreSQL continúa siendo la fuente de verdad. fileciteturn281file3

## Cómo funciona cada patrón

| Patrón | En pocas palabras |
|---|---|
| **Repository** | El caso de uso solicita operaciones como `ExisteTrabajadorConLegajoPorDniAsync()` o `AddAsync()`; la implementación concreta decide cómo consultar o persistir en PostgreSQL. |
| **Adapter** | El sistema trabaja con una interfaz propia de validación; el adaptador traduce esa operación al contrato específico de RENIEC o del servicio tributario autorizado. |
| **Dependency Injection** | Un caso de uso recibe sus dependencias mediante el constructor. `Program.cs` decide qué implementación concreta utilizar en tiempo de ejecución. |
| **Cache-Aside** | El sistema consulta primero la caché cuando el dato es apto para ello; si no existe o no es válido, consulta PostgreSQL y opcionalmente actualiza Redis. PostgreSQL conserva la autoridad del dato. |

## Ejemplo: Repository + Dependency Injection

El caso de uso trabaja únicamente con el contrato:

```csharp
public sealed class AperturarLegajoUseCase
{
    private readonly ITrabajadorRepository _trabajadores;
    private readonly ILegajoRepository _legajos;

    public AperturarLegajoUseCase(
        ITrabajadorRepository trabajadores,
        ILegajoRepository legajos)
    {
        _trabajadores = trabajadores;
        _legajos = legajos;
    }
}
```

Infrastructure proporciona la implementación concreta:

```csharp
public sealed class TrabajadorRepository : ITrabajadorRepository
{
    private readonly GestionEscalafonariaDbContext _db;

    public TrabajadorRepository(GestionEscalafonariaDbContext db)
        => _db = db;
}
```

Y la raíz de composición conecta ambas partes:

```csharp
builder.Services.AddScoped<ITrabajadorRepository, TrabajadorRepository>();
builder.Services.AddScoped<ILegajoRepository, LegajoRepository>();
builder.Services.AddScoped<AperturarLegajoUseCase>();
```

De esta forma, Application conoce contratos y no implementaciones concretas.

## Ejemplo: Adapter para integración externa

Las integraciones externas deben permanecer desacopladas del núcleo funcional. El sistema define un contrato propio:

```csharp
public interface IValidacionIdentidadService
{
    Task<ResultadoValidacionIdentidad> ValidarDniAsync(
        string dni,
        CancellationToken cancellationToken = default);
}
```

Infrastructure implementa el contrato para el proveedor correspondiente:

```csharp
public sealed class ReniecAdapter : IValidacionIdentidadService
{
    private readonly HttpClient _httpClient;

    public ReniecAdapter(HttpClient httpClient)
        => _httpClient = httpClient;

    public async Task<ResultadoValidacionIdentidad> ValidarDniAsync(
        string dni,
        CancellationToken cancellationToken = default)
    {
        // Traduce el contrato externo al modelo utilizado por la aplicación.
        // La llamada concreta dependerá del servicio autorizado disponible.
        throw new NotImplementedException();
    }
}
```

La indisponibilidad de la integración no debe impedir las operaciones principales del sistema; las validaciones pendientes se registran para revisión posterior. fileciteturn281file3

## Uso de caché

Redis no reemplaza a PostgreSQL. Su uso se limita a información que pueda reconstruirse desde la fuente principal, por ejemplo:

- sesiones activas como optimización;
- permisos efectivos consultados con frecuencia;
- determinados resultados agregados del dashboard cuando sea necesario.

El diseño vigente establece que las consultas principales del dashboard se realizan directamente sobre PostgreSQL y que Redis puede incorporarse como caché opcional, sin refrescos programados ni vistas materializadas obligatorias. fileciteturn281file3

## Beneficios

- Las reglas del negocio permanecen independientes de PostgreSQL, Redis y proveedores externos.
- Los repositorios pueden sustituirse o probarse mediante implementaciones simuladas.
- Una integración externa puede cambiar sin modificar los casos de uso que dependen del contrato.
- La inyección de dependencias concentra la selección de implementaciones concretas en la composición de la aplicación.
- Redis puede activarse o retirarse de una operación cacheable sin convertirlo en fuente de verdad.
- Los patrones refuerzan la separación de responsabilidades definida por Clean Architecture.

## Patrones que podrían incorporarse en futuras iteraciones

No se consideran obligatorios para la versión actual. Solo se aplicarían si la complejidad futura lo justifica.

| Patrón | Posible aplicación | Cuándo tendría sentido |
|---|---|---|
| **Strategy** | Generación de reportes PDF y Excel | Si se requiere intercambiar múltiples motores o estrategias de exportación bajo un mismo contrato. |
| **Factory** | Creación de propuestas o documentos según tipo | Si la construcción de objetos varía significativamente según el tipo de solicitud o documento. |
| **Facade** | Operaciones que coordinen varios módulos internos | Si aumenta la complejidad de interacción entre módulos y se necesita una interfaz interna más simple. |

La incorporación de nuevos patrones debe responder a una necesidad concreta del diseño y no únicamente a aumentar la cantidad de patrones utilizados.
