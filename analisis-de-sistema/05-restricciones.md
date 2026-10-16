# Restricciones del sistema

Las siguientes restricciones condicionan las decisiones de diseño, arquitectura e implementación del Sistema de Gestión Escalafonaria del Personal Municipal.

| IDENTIFICACIÓN | Restricción | Descripción |
|---|---|---|
| RC01 | Aplicación web | El sistema debe implementarse como una única aplicación web responsiva accesible mediante navegadores modernos. No se desarrollará una aplicación móvil nativa independiente en esta versión. |
| RC02 | Control de versiones | El código fuente y la documentación del proyecto deben gestionarse con Git y mantenerse en un repositorio de GitHub. |
| RC03 | API REST | La comunicación entre el frontend y el backend debe realizarse mediante una API REST utilizando HTTP/HTTPS y datos estructurados en JSON cuando corresponda. |
| RC04 | Frontend | La interfaz web debe desarrollarse con React 18, TypeScript y Vite, reutilizando la infraestructura frontend existente. |
| RC05 | Backend | El backend debe desarrollarse con ASP.NET Core sobre .NET 8 y conservar la organización modular por capas ya definida. |
| RC06 | Persistencia | PostgreSQL debe ser la fuente operativa y de verdad de la información del sistema. Los archivos Excel se utilizarán únicamente para migración inicial, importación controlada y exportaciones autorizadas; no deben funcionar como base de datos ni respaldo operativo. |
| RC07 | Caché | Redis podrá utilizarse para funciones de caché y optimización, pero no debe convertirse en la fuente de verdad de la información funcional ni ser obligatorio para preservar la consistencia de los datos. |
| RC08 | Organización arquitectónica | El backend debe mantener las capas API, Application, Domain e Infrastructure, respetando la regla de dependencias y evitando que Domain dependa de infraestructura o tecnologías externas. |
| RC09 | Contenedores | La solución debe continuar siendo compatible con Docker y Docker Compose, aprovechando la infraestructura técnica ya implementada. |
| RC10 | Alcance funcional | La primera versión se limita a la gestión escalafonaria. Quedan fuera del alcance planillas, remuneraciones, asistencia, biometría, presupuesto, tesorería, SIAF, vacaciones, cálculo de beneficios económicos y gestión integral de Recursos Humanos. |
| RC11 | Gestión documental acotada | La gestión de documentos se limita a documentos sustentatorios del legajo. No se implementarán mesa de partes, trámite documentario general, correspondencia institucional, OCR avanzado ni firma digital institucional en esta versión. |
| RC12 | Roles predefinidos | El sistema debe trabajar exactamente con cuatro roles predefinidos: Administrador del Sistema, Responsable de Escalafón, Trabajador y Usuario de Consulta Interna / Gerencia. No se crearán roles personalizados adicionales en esta versión. |
| RC13 | Integraciones externas | RENIEC y la validación tributaria se consideran integraciones opcionales y desacopladas. La indisponibilidad de estos servicios no debe impedir las operaciones principales del sistema; las validaciones pendientes deberán poder revisarse posteriormente. |
| RC14 | Capacidad prevista | La solución debe considerar al menos 1000 usuarios registrados. Este objetivo no implica que los 1000 usuarios deban estar conectados de manera concurrente. |
| RC15 | Evolución modular | La solución debe permitir incorporar nuevos módulos de Recursos Humanos en el futuro sin convertir la versión actual en microservicios ni rediseñar el núcleo escalafonario. |

## Nota

Las restricciones anteriores corresponden al alcance y a la infraestructura aprobados para la versión actual. Las decisiones operativas específicas de despliegue en nube, balanceo, respaldo, recuperación, RPO, RTO y retención se definirán posteriormente cuando exista una necesidad técnica u operativa validada.
