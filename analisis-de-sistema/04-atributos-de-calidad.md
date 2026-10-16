# Atributos de calidad

| IDENTIFICACIÓN | Atributo de calidad | Escenario de calidad |
|---|---|---|
| AC01 | Rendimiento | Las consultas de legajos, búsquedas de trabajadores, dashboards y generación de reportes deben responder en tiempos adecuados para el uso operativo municipal y soportar al menos 1000 usuarios registrados, sin asumir que todos estarán conectados de forma concurrente. |
| AC02 | Disponibilidad | El sistema debe mantenerse disponible durante las actividades administrativas de la municipalidad y continuar permitiendo las operaciones principales aun cuando servicios externos como RENIEC o una validación tributaria se encuentren temporalmente no disponibles. |
| AC03 | Seguridad | La información personal, laboral y documental debe estar protegida mediante autenticación, autorización y mínimo privilegio. Los permisos deben validarse en el backend; el Trabajador solo puede acceder a su propio legajo y el Usuario de Consulta Interna / Gerencia solo a información agregada autorizada. |
| AC04 | Integridad y consistencia histórica | Las operaciones que modifican información oficial deben preservar la consistencia entre trabajador, legajo, vinculaciones, contratos, asignaciones, movimientos y documentos, evitando estados parciales inconsistentes y sin destruir información histórica que deba conservarse. |
| AC05 | Trazabilidad y auditoría | Las operaciones relevantes deben registrar usuario, fecha, hora, acción y entidad afectada. Los historiales y registros de auditoría deben conservarse y no poder ser eliminados por los usuarios funcionales. |
| AC06 | Escalabilidad y mantenibilidad | La solución debe conservar una arquitectura modular y por capas que permita incorporar nuevos módulos de Recursos Humanos, realizar correcciones y evolucionar funcionalidades sin rediseñar el núcleo escalafonario ni afectar innecesariamente otros módulos. |
| AC07 | Usabilidad | La aplicación web debe ser responsiva y utilizable en computadoras de escritorio, laptops, tabletas y teléfonos móviles compatibles. Los formularios, menús, filtros, tablas y controles deben adaptarse al tamaño de pantalla y favorecer controles guiados y catálogos configurados cuando corresponda. |

## Nota

Estos atributos de calidad constituyen una síntesis académica de los requisitos no funcionales definidos para el sistema. Las medidas cuantitativas específicas de rendimiento, disponibilidad, respaldo o recuperación se definirán posteriormente cuando exista una validación técnica u operativa que las sustente.
