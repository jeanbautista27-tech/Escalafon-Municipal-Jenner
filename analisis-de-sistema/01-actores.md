# 01. Actores del sistema

## Descripción

Los actores son las personas que interactúan directamente con el Sistema de Gestión Escalafonaria del Personal Municipal. Cada actor accede a las funcionalidades del sistema de acuerdo con las responsabilidades y permisos asociados a su rol.

| Actor | Tipo | Descripción |
|---|---|---|
| Administrador del Sistema | Principal | Responsable de administrar las cuentas de usuario, roles, permisos, sesiones y aspectos de seguridad del sistema. |
| Responsable de Escalafón | Principal | Responsable de gestionar oficialmente la información escalafonaria del personal municipal y mantener actualizados los legajos de los trabajadores. |
| Trabajador municipal | Principal | Usuario que consulta su propio legajo y puede presentar solicitudes para registrar o actualizar información personal, académica y de capacitación. |
| Usuario de Consulta Interna / Gerencia | Principal | Usuario autorizado para consultar indicadores, dashboards y reportes agregados que apoyen la gestión institucional. |

## Responsabilidades

### Administrador del Sistema

- Administra las cuentas de usuario del sistema.
- Asigna los roles predefinidos a las cuentas de usuario.
- Gestiona permisos y accesos del sistema.
- Activa o desactiva cuentas de usuario.
- Restablece contraseñas cuando corresponda.
- Consulta información de auditoría y seguridad.
- No accede automáticamente a los legajos del personal por el solo hecho de tener el rol de administrador.

### Responsable de Escalafón

- Apertura y consulta los legajos de los trabajadores municipales.
- Registra y mantiene la información personal oficial del trabajador.
- Gestiona la información laboral e histórica del trabajador.
- Registra vínculos laborales, contratos, adendas, asignaciones y movimientos laborales.
- Registra formación académica, capacitaciones, méritos, deméritos y evaluaciones cuando corresponda.
- Gestiona los documentos sustentatorios asociados al legajo.
- Revisa las solicitudes de actualización presentadas por los trabajadores.
- Aprueba o rechaza las solicitudes de actualización.
- Consulta alertas relacionadas con vencimientos de contratos o vínculos laborales.
- Genera reportes y fichas escalafonarias autorizadas.
- Realiza correcciones justificadas sobre la información oficial cuando corresponda, manteniendo trazabilidad y auditoría.

### Trabajador municipal

- Inicia sesión en el sistema.
- Consulta únicamente la información correspondiente a su propio legajo.
- Consulta los documentos de su legajo que hayan sido expresamente habilitados para su visualización.
- Registra sus datos personales iniciales mediante una solicitud.
- Presenta solicitudes para actualizar información personal permitida.
- Presenta información relacionada con su formación académica y capacitación.
- Consulta el estado de las solicitudes que haya presentado.
- No modifica directamente la información oficial de su legajo.
- No accede a la información de otros trabajadores.

### Usuario de Consulta Interna / Gerencia

- Inicia sesión en el sistema.
- Consulta dashboards e indicadores institucionales.
- Consulta reportes agregados autorizados.
- Consulta información estadística para apoyar la toma de decisiones.
- No modifica información escalafonaria.
- No accede a legajos individuales.
- No accede a documentos sustentatorios individuales.
- No accede a información personal detallada de los trabajadores.

## Resumen de acceso

- El **Administrador del Sistema** administra usuarios, roles, permisos y seguridad, pero no obtiene acceso automático a los legajos.
- El **Responsable de Escalafón** gestiona la información oficial e histórica de los legajos del personal municipal.
- El **Trabajador municipal** consulta únicamente su propio legajo y presenta solicitudes de actualización sin modificar directamente la información oficial.
- El **Usuario de Consulta Interna / Gerencia** consulta únicamente dashboards, indicadores y reportes agregados autorizados, sin acceder al detalle individual de los trabajadores.
