# Patrones de diseño

## Objetivo

Documentar los patrones de diseño aplicados en el backend del Sistema de Gestión Escalafonaria del Personal Municipal, indicando dónde se usan, qué problema resuelven y con qué tecnología se implementan, para que el desarrollo mantenga una estructura uniforme.

## Contexto

- **Estilo:** monolito modular (ASP.NET Core / .NET 8).
- **Enfoque interno:** Clean Architecture.
- **Base:** diagrama de componentes y diseño interno de módulos.

## Patrones aplicados

| Patrón | Dónde se usa | Problema que resuelve | Se implementa con | Archivos / elementos en el código |
|---|---|---|---|---|
| Adapter | Integraciones → RENIEC | RENIEC posee su propio contrato de consulta y no debe acoplarse al núcleo del sistema | Cliente HTTP y adaptador en Infrastructure | `IValidacionIdentidadService`, `ReniecAdapter` |
| Adapter | Integraciones → Servicio de validación tributaria | El proveedor externo puede cambiar y posee su propia API | API REST mediante un adaptador desacoplado | `IValidacionTributariaService`, adaptador del proveedor autorizado |
| Repository | Módulos funcionales → Base de datos | El negocio no debe conocer Entity Framework Core, SQL ni PostgreSQL directamente | Entity Framework Core + Npgsql + PostgreSQL | `ITrabajadorRepository`, `ILegajoRepository`, `TrabajadorRepository`, `LegajoRepository` |
| Dependency Injection | API → Casos de uso y repositorios | Evitar que los casos de uso creen directamente implementaciones concretas | Contenedor de dependencias de ASP.NET Core | `Program.cs`, interfaces e implementaciones registradas |

## Cómo funciona cada patrón

| Patrón | En pocas palabras |
|---|---|
| Adapter | Traduce una operación interna del sistema, como validar un DNI, a la llamada específica que requiere el servicio externo. |
| Repository | El caso de uso solicita consultar o guardar información; el repositorio se encarga de acceder a PostgreSQL. |
| Dependency Injection | Los casos de uso reciben interfaces; la configuración del sistema decide qué implementación concreta utilizar. |

## Beneficio

- Cambiar un proveedor externo afecta principalmente al adaptador correspondiente y no a las reglas del negocio.
- Cambiar detalles de persistencia afecta principalmente a los repositorios, manteniendo desacoplados los casos de uso.
- La inyección de dependencias facilita sustituir implementaciones sin modificar la lógica principal del sistema.
- La separación entre contratos e implementaciones favorece el mantenimiento y las pruebas del sistema.

## Patrones previstos para siguientes iteraciones

| Patrón | Dónde se aplicaría | Cuándo |
|---|---|---|
| Strategy | Reportes → Exportación PDF / Excel | Si se requiere manejar varias estrategias de generación de reportes bajo un mismo contrato. |
| Factory | Solicitudes y documentos | Si la creación de objetos según tipo se vuelve más compleja. |
| Facade | Comunicación entre módulos | Cuando aumente la cantidad de interacciones entre módulos y se requiera una entrada interna simplificada. |
