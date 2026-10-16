# Componentes arquitectónicos

## Diagrama de componentes – Sistema de Gestión Escalafonaria

**Modelo C4 – Nivel 3 (Componentes)**  
**Estilo arquitectónico:** Monolito modular organizado por capas.

```mermaid
flowchart TB

    %% =========================
    %% ACTORES
    %% =========================
    subgraph ACT["ACTORES"]
        direction LR
        ADM["Administrador del Sistema<br/><small>Gestiona usuarios, roles, permisos y seguridad</small>"]
        RES["Responsable de Escalafón<br/><small>Gestiona la información escalafonaria oficial</small>"]
        TRA["Trabajador municipal<br/><small>Consulta su legajo y presenta solicitudes</small>"]
        GER["Usuario de Consulta Interna / Gerencia<br/><small>Consulta indicadores y reportes agregados</small>"]
    end

    %% =========================
    %% FRONTEND
    %% =========================
    WEB["Aplicación Web<br/><small>[Contenedor: React 18 + TypeScript + Vite]<br/>Interfaz responsiva según rol y permisos</small>"]

    %% =========================
    %% BACKEND
    %% =========================
    subgraph APIBACK["API Backend – Sistema de Gestión Escalafonaria<br/>[Contenedor: ASP.NET Core / .NET 8 – Monolito modular]"]
        direction TB

        API["API REST<br/><small>[Componente]<br/>Endpoints, validación de entrada, autenticación y autorización</small>"]

        subgraph MOD["MÓDULOS FUNCIONALES"]
            direction LR

            SEG["Administración y Seguridad<br/><small>[Componente]<br/>Usuarios, roles, permisos, sesiones y auditoría</small>"]

            LEG["Trabajadores y Legajos<br/><small>[Componente]<br/>Legajo, datos personales y estado del trabajador</small>"]

            LAB["Gestión Laboral e Historial<br/><small>[Componente]<br/>Vinculaciones, contratos, adendas, asignaciones y movimientos</small>"]

            DOC["Documentos y Solicitudes<br/><small>[Componente]<br/>Sustentos documentales y solicitudes de actualización</small>"]

            ORG["Organización y Catálogos<br/><small>[Componente]<br/>Unidades orgánicas y listas configurables</small>"]

            REP["Alertas, Dashboard y Reportes<br/><small>[Componente]<br/>Vencimientos, indicadores, ficha y exportaciones</small>"]

            LOC["Locadores<br/><small>[Componente]<br/>Registro independiente de locadores y servicios</small>"]

            MIG["Migración e Integraciones<br/><small>[Componente]<br/>Importación Excel y validaciones externas</small>"]
        end

        API -->|"invoca casos de uso"| SEG
        API -->|"invoca casos de uso"| LEG
        API -->|"invoca casos de uso"| LAB
        API -->|"invoca casos de uso"| DOC
        API -->|"invoca casos de uso"| ORG
        API -->|"invoca casos de uso"| REP
        API -->|"invoca casos de uso"| LOC
        API -->|"invoca casos de uso"| MIG

        LEG -->|"mantiene historial"| LAB
        DOC -->|"sustenta información"| LEG
        DOC -->|"sustenta operaciones"| LAB
        ORG -->|"provee unidades y catálogos"| LAB
        REP -->|"consulta información autorizada"| LEG
        REP -->|"consulta información autorizada"| LAB
    end

    %% =========================
    %% DATOS
    %% =========================
    DB[("PostgreSQL<br/><small>[Base de datos]<br/>Fuente de verdad del sistema</small>")]
    CACHE[("Redis<br/><small>[Caché]<br/>Apoyo para optimización</small>")]

    %% =========================
    %% EXTERNOS
    %% =========================
    RENIEC["RENIEC<br/><small>[Sistema externo]<br/>Validación de identidad</small>"]
    TRIB["Servicio de validación tributaria<br/><small>[Sistema externo]<br/>Integración opcional/autorizada</small>"]
    XLS["Archivo Excel<br/><small>[Fuente externa]<br/>Migración inicial controlada</small>"]

    %% =========================
    %% RELACIONES
    %% =========================
    ADM -->|"usa"| WEB
    RES -->|"usa"| WEB
    TRA -->|"usa"| WEB
    GER -->|"usa"| WEB

    WEB -->|"HTTPS / JSON"| API

    SEG -->|"lee / escribe"| DB
    LEG -->|"lee / escribe"| DB
    LAB -->|"lee / escribe"| DB
    DOC -->|"lee / escribe"| DB
    ORG -->|"lee / escribe"| DB
    REP -->|"consulta"| DB
    LOC -->|"lee / escribe"| DB
    MIG -->|"importa / actualiza"| DB

    REP -.->|"usa cuando corresponde"| CACHE
    SEG -.->|"puede usar caché/sesión"| CACHE

    MIG -.->|"valida identidad"| RENIEC
    MIG -.->|"valida información tributaria"| TRIB
    XLS -->|"validar → previsualizar → confirmar"| MIG

    %% =========================
    %% ESTILOS
    %% =========================
    classDef person fill:#24477f,stroke:#18345f,color:#fff,stroke-width:1px
    classDef container fill:#4472c4,stroke:#2f5597,color:#fff,stroke-width:1.5px
    classDef component fill:#8fb5e3,stroke:#5b88bd,color:#111,stroke-width:1px
    classDef database fill:#4472c4,stroke:#2f5597,color:#fff,stroke-width:1.5px
    classDef external fill:#8c8c8c,stroke:#666,color:#fff,stroke-width:1px

    class ADM,RES,TRA,GER person
    class WEB,API container
    class SEG,LEG,LAB,DOC,ORG,REP,LOC,MIG component
    class DB,CACHE database
    class RENIEC,TRIB,XLS external
```

## Descripción de los componentes

| Componente | Responsabilidad principal |
|---|---|
| **Aplicación Web** | Presenta las funcionalidades disponibles para cada actor y consume la API REST mediante HTTPS/JSON. |
| **API REST** | Expone los endpoints del sistema, recibe las solicitudes y aplica validación, autenticación y autorización antes de invocar los casos de uso. |
| **Administración y Seguridad** | Gestiona usuarios, roles, permisos, sesiones y registros de auditoría relacionados con la seguridad del sistema. |
| **Trabajadores y Legajos** | Gestiona la información principal del trabajador, el legajo escalafonario y su estado activo o pasivo. |
| **Gestión Laboral e Historial** | Administra vinculaciones laborales, contratos, adendas, asignaciones, movimientos y periodos de servicio. |
| **Documentos y Solicitudes** | Gestiona documentos sustentatorios y el flujo de solicitudes presentadas por los trabajadores. |
| **Organización y Catálogos** | Administra unidades orgánicas y listas configurables utilizadas por los demás módulos. |
| **Alertas, Dashboard y Reportes** | Calcula alertas de vencimiento y proporciona indicadores, ficha escalafonaria y reportes de acuerdo con los permisos del usuario. |
| **Locadores** | Gestiona de manera independiente los datos de locadores y sus servicios, sin convertirlos en legajos escalafonarios. |
| **Migración e Integraciones** | Ejecuta la migración inicial desde Excel y encapsula las validaciones externas mediante mecanismos desacoplados. |
| **PostgreSQL** | Es la fuente de verdad para la información oficial, histórica y transaccional del sistema. |
| **Redis** | Se utiliza únicamente como apoyo para caché u optimización cuando sea necesario. |

## Criterios arquitectónicos representados

- Los módulos forman parte de un **monolito modular** y se despliegan conjuntamente.
- El frontend se comunica con el backend exclusivamente mediante la **API REST**.
- La información oficial se conserva en **PostgreSQL**.
- **Redis** no sustituye a la base de datos principal.
- Las integraciones externas permanecen desacopladas del núcleo funcional.
- La indisponibilidad de RENIEC o del servicio de validación tributaria no debe bloquear las operaciones principales del sistema.
- Los permisos se validan en el backend y determinan qué información y operaciones puede utilizar cada actor.
