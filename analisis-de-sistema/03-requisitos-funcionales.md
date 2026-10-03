# Requisitos funcionales

| ID | Requisito funcional |
|---|---|
| RF01 | El sistema debe permitir que los usuarios inicien sesión con sus credenciales. |
| RF02 | El sistema debe permitir al administrador general registrar, consultar, actualizar y desactivar cuentas de usuario. |
| RF03 | El sistema debe permitir al administrador general asignar roles y permisos a las cuentas de usuario. |
| RF04 | El sistema debe permitir al administrador de escalafón registrar la ficha escalafonaria de cada trabajador municipal. |
| RF05 | El sistema debe permitir al administrador de escalafón actualizar la información registrada en las fichas escalafonarias. |
| RF06 | El sistema debe permitir al administrador de escalafón buscar trabajadores por sus datos de identificación. |
| RF07 | El sistema debe permitir al trabajador municipal consultar únicamente su propia ficha escalafonaria. |
| RF08 | El sistema debe permitir al administrador de escalafón registrar y actualizar áreas, cargos y plazas. |
| RF09 | El sistema debe permitir al administrador de escalafón asociar a cada trabajador con su área, cargo y plaza correspondiente. |
| RF10 | El sistema debe permitir al administrador de escalafón actualizar la condición laboral de los trabajadores. |
| RF11 | El sistema debe permitir al administrador de escalafón registrar capacitaciones y certificaciones de los trabajadores. |
| RF12 | El sistema debe permitir al trabajador municipal consultar las capacitaciones y certificaciones registradas en su ficha. |
| RF13 | El sistema debe permitir al administrador de escalafón generar reportes del personal por área, cargo y condición laboral. |
| RF14 | El sistema debe permitir al administrador de escalafón consultar reportes sobre las plazas ocupadas y disponibles por área. |
| RF15 | El sistema debe mostrar al administrador de escalafón alertas de trabajadores próximos a jubilarse, según los criterios establecidos. |

## Relación entre historias de usuario y requisitos funcionales

| Historia de usuario | Requisitos relacionados |
|---|---|
| HU01: Gestionar usuarios y permisos | RF01, RF02, RF03 |
| HU02: Registrar ficha escalafonaria | RF04 |
| HU03: Actualizar ficha escalafonaria | RF05, RF10 |
| HU04: Buscar y consultar ficha | RF06 |
| HU05: Consultar mi ficha | RF07 |
| HU06: Gestionar plazas y asignaciones | RF08, RF09 |
| HU07: Registrar capacitaciones y certificaciones | RF11 |
| HU08: Consultar mi historial de formación | RF12 |
| HU09: Generar reportes del personal | RF13, RF14 |
| HU10: Consultar alertas de jubilación | RF15 |

**Nota:** El requisito RF01 es una condición de acceso común; los usuarios deben iniciar sesión para utilizar las funciones correspondientes a su rol.