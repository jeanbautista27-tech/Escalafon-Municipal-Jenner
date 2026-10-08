cat > analisis-de-sistema/07-decisiones-arquitectonicas.md <<'EOF'
# Decisiones arquitectónicas

Las decisiones arquitectónicas responden a los drivers identificados para el Sistema de Gestión Escalafonaria Municipal y establecen cómo se organizará técnicamente el sistema.

Un ADR (Architecture Decision Record) registra una decisión importante, el driver que la origina, su justificación y el resultado esperado.

| ID | Decisión arquitectónica | Driver relacionado | Justificación | Resultado |
|---|---|---|---|---|
| ADR-001 | Monolito modular | DA05 - Organización modular; DA08 - Alcance e integraciones | Organizar las funcionalidades del escalafón en módulos relacionados, manteniendo una aplicación desplegable. | Módulos de trabajadores, legajos, plazas, capacitaciones, reportes y usuarios. |
| ADR-002 | Clean Architecture | DA05 - Organización modular | Separar las responsabilidades del backend y las reglas del negocio de los detalles técnicos. | Capas API, Application, Domain e Infrastructure. |
| ADR-003 | API REST para comunicar frontend y backend | DA04 - API REST y comunicación entre frontend y backend | Definir una forma clara de comunicación entre la interfaz web y los servicios del backend. | El frontend React consume endpoints REST del backend ASP.NET Core mediante solicitudes HTTP y respuestas JSON. |
| ADR-004 | PostgreSQL para persistencia y Redis para caché | DA02 - Rendimiento; DA06 - Base de datos y caché | Atender consultas frecuentes con tiempos adecuados y separar los datos permanentes de la información temporal en caché. | PostgreSQL almacena la información del sistema y Redis mantiene temporalmente datos seleccionados de consulta frecuente. |
| ADR-005 | Control de acceso basado en roles | DA03 - Seguridad | Proteger la información personal y laboral y limitar el acceso según las responsabilidades de cada usuario. | Permisos diferenciados para el administrador general, el administrador de escalafón y el trabajador municipal. |
| ADR-006 | Despliegue en contenedores con balanceo de carga | DA01 - Escalabilidad y capacidad para 1000 usuarios; DA07 - Disponibilidad, contenedores y balanceador | Facilitar el despliegue de los servicios y distribuir el tráfico cuando existan varias instancias de la aplicación. | Servicios desplegados con Docker y Docker Compose; AWS Application Load Balancer considerado para distribuir solicitudes en AWS. |
| ADR-007 | Incorporación gradual de módulos e integraciones | DA08 - Alcance e integraciones | Enfocar la primera versión en el escalafón municipal y permitir ampliar el sistema posteriormente. | El sistema inicia con funcionalidades de escalafón y podrá incorporar módulos o integraciones institucionales mediante componentes desacoplados. |

## Tecnologías relacionadas

| Componente | Tecnología propuesta |
|---|---|
| Interfaz web | React + TypeScript |
| Backend y API REST | ASP.NET Core / .NET 8 |
| Base de datos | PostgreSQL |
| Caché | Redis |
| Contenedores | Docker y Docker Compose |
| Balanceador de carga previsto para AWS | AWS Application Load Balancer |

