# Restricciones del sistema

Las siguientes restricciones condicionan las decisiones de diseño, arquitectura e implementación del Sistema de Gestión Escalafonaria del Personal Municipal.

| IDENTIFICACIÓN | Restricción | Descripción |
|---|---|---|
| RC01 | Aplicación web | El sistema debe implementarse como una aplicación web responsiva accesible mediante navegadores modernos. No se desarrollará una aplicación móvil nativa independiente en esta versión. |
| RC02 | API REST | La comunicación entre el frontend y el backend debe realizarse mediante una API REST utilizando HTTP/HTTPS y datos estructurados en JSON cuando corresponda. |
| RC03 | Stack tecnológico | La interfaz web debe desarrollarse con React 18, TypeScript y Vite, mientras que el backend debe implementarse con ASP.NET Core sobre .NET 8, reutilizando la infraestructura técnica existente. |
| RC04 | Persistencia | PostgreSQL debe ser la fuente operativa y de verdad de la información del sistema. Redis podrá utilizarse únicamente como apoyo para caché u optimización y no como fuente principal de datos. |
| RC05 | Organización arquitectónica | El backend debe mantener una arquitectura modular por capas: API, Application, Domain e Infrastructure, respetando la regla de dependencias y evitando que Domain dependa de infraestructura o tecnologías externas. |
| RC06 | Alcance funcional | La primera versión se limita a la gestión escalafonaria. Quedan fuera del alcance planillas, remuneraciones, asistencia, biometría, presupuesto, tesorería, SIAF, vacaciones, cálculo de beneficios económicos y gestión integral de Recursos Humanos. La gestión documental se limita a documentos sustentatorios del legajo. |
| RC07 | Roles predefinidos | El sistema debe trabajar exactamente con cuatro roles predefinidos: Administrador del Sistema, Responsable de Escalafón, Trabajador y Usuario de Consulta Interna / Gerencia. No se crearán roles personalizados adicionales en esta versión. |
| RC08 | Integraciones externas | RENIEC y la validación tributaria se consideran integraciones opcionales y desacopladas. La indisponibilidad de estos servicios no debe impedir las operaciones principales del sistema. |
| RC09 | Capacidad prevista | La solución debe considerar al menos 1000 usuarios registrados. Este objetivo no implica que los 1000 usuarios deban estar conectados de manera concurrente. |

## Nota

Las restricciones anteriores resumen únicamente las condiciones que influyen de forma directa en la arquitectura y el alcance de la versión actual. Aspectos como control de versiones, contenedores, despliegue en nube, respaldo y recuperación se documentarán en las secciones técnicas correspondientes cuando sea necesario.
