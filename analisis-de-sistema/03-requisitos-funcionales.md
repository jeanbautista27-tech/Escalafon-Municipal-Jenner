# Requisitos funcionales

| IDENTIFICACIÓN | Requisito funcional |
|---|---|
| RF01 | El sistema debe permitir que los usuarios inicien sesión con sus credenciales y accedan únicamente a las funcionalidades autorizadas para sus roles. |
| RF02 | El sistema debe permitir cerrar sesión e invalidar la sesión activa del usuario. |
| RF03 | El sistema debe permitir al Administrador del Sistema registrar, consultar, actualizar, activar y desactivar cuentas de usuario. |
| RF04 | El sistema debe permitir al Administrador del Sistema asignar a las cuentas uno o más de los cuatro roles predefinidos: Administrador del Sistema, Responsable de Escalafón, Trabajador y Usuario de Consulta Interna / Gerencia. |
| RF05 | El sistema debe registrar y permitir consultar la auditoría de las operaciones relevantes realizadas por los usuarios. |
| RF06 | El sistema debe permitir al Responsable de Escalafón aperturar un legajo para un trabajador a partir de su DNI, evitando la creación de un segundo legajo para el mismo trabajador. |
| RF07 | El sistema debe permitir al Responsable de Escalafón buscar trabajadores por DNI y otros criterios de identificación disponibles. |
| RF08 | El sistema debe permitir al Responsable de Escalafón consultar el legajo completo y su historial, de acuerdo con sus permisos. |
| RF09 | El sistema debe permitir al Responsable de Escalafón registrar y mantener la información personal oficial del trabajador, conservando la trazabilidad de los cambios. |
| RF10 | El sistema debe permitir al Responsable de Escalafón gestionar las vinculaciones laborales del trabajador y distinguir explícitamente cuál representa su situación laboral actual. |
| RF11 | El sistema debe permitir al Responsable de Escalafón registrar contratos primigenios y sus adendas, manteniendo el historial correspondiente. |
| RF12 | El sistema debe permitir al Responsable de Escalafón registrar asignaciones organizacionales y conservar el historial de asignaciones del trabajador. |
| RF13 | El sistema debe permitir al Responsable de Escalafón registrar movimientos laborales, incluyendo el tipo de movimiento, unidades de origen y destino, cargos, documento sustentatorio y observaciones cuando corresponda. |
| RF14 | El sistema debe permitir registrar y consultar formación académica, capacitaciones, méritos, deméritos y evaluaciones asociadas al trabajador. |
| RF15 | El sistema debe permitir al Responsable de Escalafón cargar, clasificar, asociar, verificar, inactivar, anular o reemplazar documentos sustentatorios sin eliminar físicamente el historial documental oficial. |
| RF16 | El sistema debe permitir asociar documentos sustentatorios con el legajo, solicitudes de actualización, periodos de servicio y demás entidades autorizadas, manteniendo su trazabilidad. |
| RF17 | El sistema debe permitir al Trabajador municipal consultar únicamente su propio legajo y los documentos que hayan sido expresamente habilitados para su visualización. |
| RF18 | El sistema debe permitir al Trabajador municipal registrar sus datos personales iniciales y presentar solicitudes de actualización de información personal permitida, formación académica y capacitación. |
| RF19 | El sistema debe permitir al Responsable de Escalafón revisar, aprobar o rechazar las solicitudes presentadas por los trabajadores, actualizando la información oficial únicamente cuando la solicitud sea aprobada. |
| RF20 | El sistema debe permitir al Responsable de Escalafón gestionar unidades orgánicas jerárquicas, incluyendo su activación, inactivación e historial. |
| RF21 | El sistema debe permitir al Responsable de Escalafón gestionar catálogos configurables utilizados por el sistema, tales como régimen laboral, condición laboral, estado laboral, profesión, especialidad, cargo y tipo de movimiento. |
| RF22 | El sistema debe mostrar alertas internas sobre contratos y vinculaciones laborales próximos a vencer o vencidos, aplicando la regla establecida de días restantes. |
| RF23 | El sistema debe permitir al Responsable de Escalafón generar la ficha escalafonaria y reportes autorizados en formatos PDF y Excel. |
| RF24 | El sistema debe permitir generar reportes e indicadores por régimen laboral, condición laboral, unidad orgánica, movimientos, perfil profesional y vencimientos, según corresponda. |
| RF25 | El sistema debe permitir al Usuario de Consulta Interna / Gerencia consultar dashboards, indicadores y reportes agregados autorizados sin acceder a legajos individuales, documentos sustentatorios ni información personal detallada. |
| RF26 | El sistema debe permitir al Responsable de Escalafón registrar locadores y sus servicios en un contexto separado del legajo escalafonario, permitiendo múltiples servicios por locador. |
| RF27 | El sistema debe permitir registrar la participación histórica de personal en inversiones como un contexto independiente, sin tratarla como régimen o condición laboral. |
| RF28 | El sistema debe permitir validar y previsualizar los datos de una migración desde Excel antes de incorporarlos a la base de datos oficial. |
| RF29 | El sistema debe permitir confirmar explícitamente una importación previamente validada, resolviendo identidades, detectando inconsistencias y registrando la trazabilidad de la migración. |
| RF30 | El sistema debe permitir realizar validaciones externas de identidad mediante RENIEC y validaciones tributarias mediante un servicio autorizado cuando dichas integraciones se encuentren disponibles, sin bloquear el funcionamiento principal ante una indisponibilidad externa. |
| RF31 | El sistema debe registrar las validaciones externas que no pudieron completarse y permitir su posterior revisión o procesamiento por el Responsable de Escalafón. |
| RF32 | El sistema debe permitir registrar periodos de servicio computables y no computables y calcular el tiempo de servicios por régimen, evitando sumar automáticamente periodos de regímenes distintos y detectando periodos superpuestos. |

## Relación entre historias de usuario y requisitos funcionales

| Historia de usuario | Requisitos relacionados |
|---|---|
| HU01: Gestionar cuentas de usuario, roles y accesos | RF01, RF02, RF03, RF04 |
| HU02: Consultar auditoría y seguridad | RF05 |
| HU03: Aperturar, buscar y consultar legajos | RF06, RF07, RF08 |
| HU04: Mantener información personal oficial y laboral | RF09, RF10, RF32 |
| HU05: Gestionar historial laboral | RF10, RF11, RF12, RF13, RF32 |
| HU06: Registrar trayectoria institucional y profesional | RF14 |
| HU07: Gestionar documentos sustentatorios | RF15, RF16 |
| HU08: Consultar mi propio legajo | RF17 |
| HU09: Presentar solicitudes de actualización | RF18 |
| HU10: Revisar y resolver solicitudes | RF19 |
| HU11: Gestionar unidades orgánicas y catálogos | RF20, RF21 |
| HU12: Consultar alertas de vencimiento | RF22 |
| HU13: Generar fichas y reportes autorizados | RF23, RF24 |
| HU14: Consultar información agregada para gestión | RF24, RF25 |
| HU15: Registrar locadores y sus servicios | RF26 |
| HU16: Registrar participación histórica en inversiones | RF27 |
| HU17: Validar y confirmar migración desde Excel | RF28, RF29, RF30, RF31 |

**Nota:** RF01 y RF02 son requisitos de acceso comunes para los usuarios autenticados. La funcionalidad disponible después del inicio de sesión depende de los roles y permisos asignados a cada cuenta. El Administrador del Sistema no obtiene acceso automático a los legajos por el solo hecho de administrar la plataforma.
