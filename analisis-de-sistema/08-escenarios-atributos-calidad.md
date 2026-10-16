# Escenarios de atributos de calidad

Los siguientes escenarios permiten describir cómo deben manifestarse y verificarse los atributos de calidad definidos para el Sistema de Gestión Escalafonaria del Personal Municipal.

## EQ-01. Rendimiento: consulta y búsqueda de información escalafonaria

| Elemento | Descripción |
|---|---|
| **Atributo de calidad** | Rendimiento |
| **Fuente** | Responsable de Escalafón, Trabajador o Usuario de Consulta Interna / Gerencia |
| **Estímulo** | El usuario realiza una búsqueda de trabajadores, consulta un legajo, visualiza el dashboard o genera un reporte. |
| **Condición** | El sistema opera con un volumen representativo de información y considera al menos 1000 usuarios registrados, sin asumir que todos se encuentran conectados simultáneamente. |
| **Respuesta esperada** | El sistema procesa la solicitud y presenta la información solicitada sin errores inesperados ni degradación que impida el uso operativo normal. |
| **Medida** | La meta cuantitativa de tiempo de respuesta se definirá posteriormente mediante pruebas de rendimiento sobre un entorno y volumen de datos representativos. |
| **Verificación** | Ejecutar pruebas de rendimiento sobre búsquedas, consultas de legajos, dashboard y reportes, registrando tiempos de respuesta y errores. |
| **Estado** | Pendiente de validar una meta cuantitativa de rendimiento. |

## EQ-02. Disponibilidad: continuidad ante indisponibilidad de servicios externos

| Elemento | Descripción |
|---|---|
| **Atributo de calidad** | Disponibilidad |
| **Fuente** | Servicio externo de validación |
| **Estímulo** | RENIEC o el servicio de validación tributaria no se encuentra disponible temporalmente. |
| **Condición** | Un usuario autorizado realiza una operación principal del sistema escalafonario que puede continuar sin la respuesta inmediata del servicio externo. |
| **Respuesta esperada** | El sistema continúa con las operaciones principales que no dependen obligatoriamente del servicio externo y registra la validación como pendiente cuando corresponda. |
| **Medida** | Las pruebas de indisponibilidad deben comprobar que la caída de un servicio externo no bloquea las operaciones principales definidas como independientes de dicha integración. |
| **Verificación** | Simular indisponibilidad de las integraciones externas y comprobar la continuidad del flujo principal y el registro de validaciones pendientes. |
| **Estado** | Definido para la versión actual. |

## EQ-03. Seguridad: acceso a información protegida

| Elemento | Descripción |
|---|---|
| **Atributo de calidad** | Seguridad |
| **Fuente** | Usuario autenticado sin permisos suficientes o usuario que intenta acceder a información ajena |
| **Estímulo** | El usuario intenta consultar o modificar un recurso para el cual no posee autorización. |
| **Condición** | Se prueban operaciones protegidas sobre legajos, documentos, administración, dashboard y reportes. |
| **Respuesta esperada** | El backend rechaza la operación, no realiza cambios y no expone información protegida. |
| **Medida** | El 100 % de los casos de acceso no autorizado definidos en las pruebas debe ser rechazado sin exposición de datos sensibles. |
| **Verificación** | Ejecutar pruebas de autorización por rol y recurso, incluyendo Trabajador sobre legajo ajeno, Administrador del Sistema sin rol funcional y Usuario de Consulta sobre información individual. |
| **Estado** | Definido para la versión actual. |

## EQ-04. Integridad y consistencia histórica: actualización de información oficial

| Elemento | Descripción |
|---|---|
| **Atributo de calidad** | Integridad y consistencia histórica |
| **Fuente** | Responsable de Escalafón o proceso autorizado |
| **Estímulo** | Se registra o modifica información oficial relacionada con un trabajador, su legajo, vinculación, contrato, asignación, movimiento o documento. |
| **Condición** | La operación afecta uno o varios registros relacionados y puede requerir una transacción. |
| **Respuesta esperada** | El sistema mantiene relaciones válidas, evita estados parciales inconsistentes y conserva la información histórica que corresponda. |
| **Medida** | Las operaciones transaccionales deben finalizar de forma completa o revertirse sin dejar datos parciales; las pruebas de integridad no deben producir registros huérfanos o históricos eliminados. |
| **Verificación** | Ejecutar pruebas de restricciones, transacciones e historial sobre operaciones que afecten múltiples entidades relacionadas. |
| **Estado** | Definido para la versión actual. |

## EQ-05. Trazabilidad y auditoría: registro de operaciones relevantes

| Elemento | Descripción |
|---|---|
| **Atributo de calidad** | Trazabilidad y auditoría |
| **Fuente** | Usuario autorizado del sistema |
| **Estímulo** | El usuario realiza una operación relevante, como iniciar o cerrar sesión, modificar información oficial, resolver una solicitud, corregir un dato sensible o generar un reporte. |
| **Condición** | La operación se completa o produce un cambio que debe quedar registrado. |
| **Respuesta esperada** | El sistema registra usuario, fecha, hora, tipo de operación, entidad afectada y detalles necesarios para rastrear la acción. |
| **Medida** | Todas las operaciones catalogadas como auditables deben generar su correspondiente registro de auditoría o historial y dichos registros no deben poder ser eliminados por usuarios funcionales. |
| **Verificación** | Ejecutar operaciones auditables y comprobar la existencia, contenido y permanencia de los registros generados. |
| **Estado** | Definido para la versión actual. |

## EQ-06. Escalabilidad y mantenibilidad: incorporación o cambio de funcionalidades

| Elemento | Descripción |
|---|---|
| **Atributo de calidad** | Escalabilidad y mantenibilidad |
| **Fuente** | Equipo de desarrollo |
| **Estímulo** | Se modifica una regla del dominio escalafonario o se incorpora una nueva funcionalidad o módulo relacionado con Recursos Humanos. |
| **Condición** | El sistema conserva una arquitectura modular y por capas con responsabilidades separadas. |
| **Respuesta esperada** | El cambio se concentra en el módulo y capas correspondientes sin requerir rediseñar el núcleo completo ni introducir dependencias indebidas entre módulos. |
| **Medida** | Las pruebas del módulo modificado y las pruebas de regresión relacionadas deben aprobarse, y las dependencias deben respetar las reglas arquitectónicas definidas. |
| **Verificación** | Revisar cambios de código, dependencias entre proyectos/capas y resultados de pruebas automatizadas. |
| **Estado** | Definido para la versión actual. |

## EQ-07. Usabilidad: operación desde distintos dispositivos

| Elemento | Descripción |
|---|---|
| **Atributo de calidad** | Usabilidad |
| **Fuente** | Responsable de Escalafón, Trabajador o Usuario de Consulta Interna / Gerencia |
| **Estímulo** | El usuario accede al sistema desde un equipo de escritorio, laptop, tableta o teléfono móvil compatible. |
| **Condición** | Se utilizan las principales pantallas, formularios, menús, filtros y tablas del sistema. |
| **Respuesta esperada** | La interfaz reorganiza sus elementos de acuerdo con el espacio disponible y mantiene utilizables las funciones correspondientes al actor. |
| **Medida** | Las funciones críticas del Trabajador deben poder utilizarse en dispositivos móviles compatibles y las operaciones administrativas deben mantenerse utilizables en escritorio y otros tamaños soportados. |
| **Verificación** | Realizar pruebas de interfaz en diferentes tamaños de pantalla y verificar navegación, formularios, filtros, tablas y controles principales. |
| **Estado** | Definido para la versión actual. |

## Resumen de escenarios

| Código | Atributo de calidad | Qué se busca comprobar |
|---|---|---|
| EQ-01 | Rendimiento | Que las consultas y operaciones principales respondan adecuadamente al volumen operativo previsto. |
| EQ-02 | Disponibilidad | Que la indisponibilidad de integraciones externas no bloquee el núcleo del sistema. |
| EQ-03 | Seguridad | Que ningún usuario acceda a funciones o información para las que no está autorizado. |
| EQ-04 | Integridad y consistencia histórica | Que los cambios mantengan datos consistentes y conserven el historial necesario. |
| EQ-05 | Trazabilidad y auditoría | Que las operaciones relevantes puedan rastrearse y sus registros se conserven. |
| EQ-06 | Escalabilidad y mantenibilidad | Que el sistema pueda evolucionar sin rediseñar ni afectar innecesariamente otros módulos. |
| EQ-07 | Usabilidad | Que la aplicación continúe siendo utilizable en los dispositivos y tamaños de pantalla previstos. |
