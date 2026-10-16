# Decisiones arquitectónicas

Las decisiones arquitectónicas responden a los drivers identificados para el Sistema de Gestión Escalafonaria del Personal Municipal y definen cómo se organizará técnicamente la solución.

| ID | Decisión arquitectónica | Driver relacionado | Justificación | Resultado |
|---|---|---|---|---|
| ADR-001 | Monolito modular | DA03 – Modularidad y mantenibilidad | Permite organizar las funcionalidades escalafonarias en módulos claramente separados dentro de una sola aplicación desplegable, evitando la complejidad innecesaria de microservicios en esta etapa. | El backend se implementará como un monolito modular con módulos funcionales desacoplados y límites de responsabilidad definidos. |
| ADR-002 | Clean Architecture | DA02 – Integridad y trazabilidad; DA03 – Modularidad y mantenibilidad | Se requiere separar las reglas del negocio de los detalles técnicos para facilitar mantenimiento, pruebas y evolución del sistema. | El backend mantendrá las capas API, Application, Domain e Infrastructure, y el dominio no dependerá de tecnologías externas. |
| ADR-003 | API REST entre frontend y backend | DA06 – Comunicación cliente-servidor | La aplicación web necesita un contrato claro y desacoplado para comunicarse con los servicios del backend. | El frontend React consumirá endpoints REST del backend ASP.NET Core mediante HTTP/HTTPS y JSON. |
| ADR-004 | PostgreSQL como fuente de verdad y Redis como apoyo | DA04 – Rendimiento; DA07 – Persistencia | La información escalafonaria requiere persistencia relacional, integridad y conservación histórica. Redis puede optimizar consultas, pero no debe sustituir a la base de datos principal. | PostgreSQL almacenará la información oficial del sistema y Redis se utilizará únicamente para caché u optimizaciones cuando sea necesario. |
| ADR-005 | Autenticación con JWT y sesiones revocables, con autorización por roles y permisos | DA01 – Seguridad y control de acceso; DA02 – Trazabilidad | El sistema maneja información personal y laboral sensible y necesita controlar tanto quién accede como qué operaciones puede ejecutar cada usuario. | Se utilizarán JWT asociados a sesiones revocables y se aplicará autorización por roles y permisos efectivos, respetando las restricciones de acceso de los cuatro roles predefinidos. |
| ADR-006 | Integraciones externas mediante interfaces y adaptadores | DA05 – Disponibilidad ante fallos externos; DA03 – Modularidad y mantenibilidad | RENIEC y la validación tributaria no deben acoplarse al núcleo del negocio ni bloquear las operaciones principales cuando no estén disponibles. | Las integraciones externas se implementarán mediante contratos en Application y adaptadores en Infrastructure, registrando validaciones pendientes cuando corresponda. |
| ADR-007 | Aplicación web responsiva por funcionalidades | DA08 – Usabilidad; DA03 – Modularidad y mantenibilidad | Los distintos actores necesitan utilizar el sistema desde diferentes tamaños de pantalla sin crear una aplicación móvil separada. | El frontend se organizará por funcionalidades y utilizará componentes responsivos, priorizando escritorio para operaciones administrativas complejas y acceso móvil para funciones del trabajador. |

## Tecnologías relacionadas

| Componente | Tecnología |
|---|---|
| Interfaz web | React 18 + TypeScript + Vite |
| Backend y API REST | ASP.NET Core / .NET 8 |
| Persistencia principal | PostgreSQL |
| Caché | Redis |
| Contenedores | Docker y Docker Compose |
