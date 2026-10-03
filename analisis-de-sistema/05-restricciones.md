# Restricciones del sistema

| ID | Restricción | Descripción |
|---|---|---|
| RC01 | Aplicación web | El sistema debe estar disponible mediante un navegador web. |
| RC02 | Control de versiones | El código y la documentación del proyecto deben gestionarse con Git y mantenerse en el repositorio de GitHub. |
| RC03 | API REST | La comunicación entre el frontend y el backend debe realizarse mediante una API REST. |
| RC04 | Frontend | La interfaz web se desarrollará con React y TypeScript. |
| RC05 | Backend | Los servicios del sistema se desarrollarán con ASP.NET Core y .NET 8, organizados con Clean Architecture. |
| RC06 | Base de datos y caché | PostgreSQL se utilizará para almacenar la información y Redis para las funciones de caché previstas. |
| RC07 | Organización arquitectónica | El backend debe mantener una estructura modular en las capas API, Application, Domain e Infrastructure. |
| RC08 | Contenedores | Docker y Docker Compose se utilizarán para preparar y ejecutar los servicios del sistema. |
| RC09 | Capacidad prevista | La propuesta debe considerar el objetivo del curso de atender al menos a 1000 usuarios. |
| RC10 | Balanceador de carga | La propuesta de despliegue debe considerar AWS Application Load Balancer como balanceador de carga. |
| RC11 | Alcance e integraciones | La primera versión se enfocará en el sistema escalafonario; las integraciones con otros módulos se incorporarán gradualmente. |