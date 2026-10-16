# Enfoque arquitectónico

## 1. Descripción

El Sistema de Gestión Escalafonaria del Personal Municipal adopta **Clean Architecture** para separar las reglas del negocio de los detalles de presentación, persistencia, caché e integraciones externas.

El backend se implementa como un **monolito modular** sobre ASP.NET Core / .NET 8. La dirección de las dependencias apunta hacia el núcleo: **Domain** no depende de otras capas, **Application** depende de Domain, **Infrastructure** implementa contratos definidos por Application y **API** expone los casos de uso.

## 2. Patrón seleccionado

| Aspecto | Descripción |
|---|---|
| Patrón arquitectónico | Clean Architecture |
| Estilo de implementación | Monolito modular |
| Objetivo | Mantener las reglas del negocio independientes de frameworks, base de datos e integraciones externas. |
| Capas principales | API, Application, Domain e Infrastructure |
| Regla principal | Las dependencias de código deben apuntar hacia Domain y Application. |
| Beneficio | Facilita mantenimiento, pruebas, evolución e incorporación de nuevas integraciones sin modificar el núcleo del negocio. |

## 3. Diagrama del enfoque arquitectónico

El siguiente diagrama representa la estructura del backend siguiendo una organización semejante a Clean Architecture, mostrando presentación, casos de uso, dominio, contratos, adaptadores e infraestructura.

```mermaid
flowchart LR

    %% =========================================================
    %% USUARIOS Y CLIENTE WEB
    %% =========================================================
    USER["Usuarios del sistema<br/><small>Administrador · Responsable de Escalafón<br/>Trabajador · Consulta Interna / Gerencia</small>"]
    WEB["Aplicación Web<br/><small>React 18 + TypeScript + Vite</small>"]

    USER -->|"navegador"| WEB

    %% =========================================================
    %% BACKEND
    %% =========================================================
    subgraph BACKEND["«aplicación» Sistema de Gestión Escalafonaria – Backend ASP.NET Core / .NET 8"]
        direction TB

        %% -----------------------------------------------------
        %% ADAPTADORES Y FRAMEWORKS
        %% -----------------------------------------------------
        subgraph FRAME["ADAPTADORES Y FRAMEWORKS"]
            direction LR

            %% PRESENTACION
            subgraph PRES["PRESENTACIÓN – API"]
                direction TB
                CONTROLLERS["«componente»<br/>Controllers / Endpoints<br/><small>Reciben solicitudes HTTP</small>"]
                AUTH["«componente»<br/>Autenticación y Autorización<br/><small>JWT, sesiones, roles y permisos</small>"]
                VALID["«componente»<br/>Validación y manejo de errores<br/><small>Entrada, respuestas y middleware</small>"]
            end

            %% NUCLEO
            subgraph CORE["NÚCLEO DE LA APLICACIÓN"]
                direction TB

                subgraph APP["APPLICATION – Casos de uso y contratos"]
                    direction TB

                    subgraph USES["Casos de uso"]
                        direction LR
                        UC1["«caso de uso»<br/>Gestionar Legajo"]
                        UC2["«caso de uso»<br/>Gestionar Historia Laboral"]
                        UC3["«caso de uso»<br/>Resolver Solicitud"]
                        UC4["«caso de uso»<br/>Generar Reporte"]
                    end

                    subgraph PORTS["Contratos / Puertos"]
                        direction LR
                        P1["«interface»<br/>Repositorios"]
                        P2["«interface»<br/>Servicio de Caché"]
                        P3["«interface»<br/>Validación Externa"]
                        P4["«interface»<br/>Auditoría / Tiempo"]
                    end
                end

                subgraph DOMAIN["DOMAIN – Núcleo del negocio"]
                    direction TB

                    subgraph ENT["Entidades y conceptos"]
                        direction LR
                        E1["Trabajador<br/><small>identidad y datos oficiales</small>"]
                        E2["Legajo<br/><small>estado e historial</small>"]
                        E3["Vinculación Laboral<br/><small>periodos y situación actual</small>"]
                        E4["Contrato / Adenda<br/><small>sustento de vínculo</small>"]
                        E5["Documento<br/><small>sustento escalafonario</small>"]
                        E6["Solicitud<br/><small>propuesta y resolución</small>"]
                    end

                    RULES["Reglas de dominio<br/><small>un legajo por trabajador · un vínculo actual<br/>historial preservado · periodos computables<br/>permisos funcionales y consistencia</small>"]
                end
            end

            %% INFRAESTRUCTURA
            subgraph INFRA["INFRASTRUCTURE – Adaptadores"]
                direction TB
                REPO["«adaptador»<br/>Persistencia<br/><small>Entity Framework Core + Npgsql</small>"]
                CACHEAD["«adaptador»<br/>Caché<br/><small>Redis</small>"]
                EXTAD["«adaptador»<br/>Validaciones externas<br/><small>RENIEC / servicio tributario</small>"]
                AUDAD["«adaptador»<br/>Auditoría y servicios técnicos"]
            end
        end

        %% -----------------------------------------------------
        %% COMPOSICION
        %% -----------------------------------------------------
        COMPOSE["«raíz de composición»<br/>Program.cs / Dependency Injection<br/><small>Registra implementaciones y resuelve dependencias</small>"]

        %% FLUJO INTERNO
        CONTROLLERS -->|"invoca"| UC1
        CONTROLLERS -->|"invoca"| UC2
        CONTROLLERS -->|"invoca"| UC3
        CONTROLLERS -->|"invoca"| UC4

        AUTH --> CONTROLLERS
        VALID --> CONTROLLERS

        UC1 -->|"aplica reglas"| DOMAIN
        UC2 -->|"aplica reglas"| DOMAIN
        UC3 -->|"aplica reglas"| DOMAIN
        UC4 -->|"consulta reglas y datos"| DOMAIN

        UC1 -.->|"depende de"| P1
        UC2 -.->|"depende de"| P1
        UC3 -.->|"depende de"| P1
        UC3 -.->|"depende de"| P4
        UC4 -.->|"depende de"| P1
        UC4 -.->|"depende de"| P2

        REPO -.->|"implementa"| P1
        CACHEAD -.->|"implementa"| P2
        EXTAD -.->|"implementa"| P3
        AUDAD -.->|"implementa"| P4

        COMPOSE -.->|"registra"| REPO
        COMPOSE -.->|"registra"| CACHEAD
        COMPOSE -.->|"registra"| EXTAD
        COMPOSE -.->|"registra"| AUDAD
    end

    %% =========================================================
    %% SISTEMAS EXTERNOS
    %% =========================================================
    DB[("PostgreSQL<br/><small>Fuente de verdad</small>")]
    REDIS[("Redis<br/><small>Caché</small>")]
    RENIEC["RENIEC<br/><small>Sistema externo</small>"]
    TAX["Servicio de validación tributaria<br/><small>Sistema externo / autorizado</small>"]

    WEB -->|"HTTPS / JSON"| CONTROLLERS

    REPO -->|"SQL"| DB
    CACHEAD -->|"lectura / escritura de caché"| REDIS
    EXTAD -->|"validación"| RENIEC
    EXTAD -->|"validación"| TAX

    %% =========================================================
    %% ESTILOS
    %% =========================================================
    classDef presentation fill:#dbeafe,stroke:#2563eb,color:#111827,stroke-width:1.5px
    classDef application fill:#dcfce7,stroke:#16a34a,color:#111827,stroke-width:1.5px
    classDef domain fill:#fef3c7,stroke:#d97706,color:#111827,stroke-width:1.5px
    classDef infrastructure fill:#ede9fe,stroke:#7c3aed,color:#111827,stroke-width:1.5px
    classDef external fill:#f3f4f6,stroke:#6b7280,color:#111827,stroke-width:1.5px
    classDef compose fill:#ffffff,stroke:#374151,color:#111827,stroke-width:1.5px

    class CONTROLLERS,AUTH,VALID presentation
    class UC1,UC2,UC3,UC4,P1,P2,P3,P4 application
    class E1,E2,E3,E4,E5,E6,RULES domain
    class REPO,CACHEAD,EXTAD,AUDAD infrastructure
    class DB,REDIS,RENIEC,TAX,USER,WEB external
    class COMPOSE compose

    style BACKEND fill:#ffffff,stroke:#111827,stroke-width:2px,stroke-dasharray:7 5
    style FRAME fill:#ffffff,stroke:#6b7280,stroke-width:1px
    style PRES fill:#eff6ff,stroke:#2563eb,stroke-width:1px
    style CORE fill:#f9fafb,stroke:#16a34a,stroke-width:1px
    style APP fill:#f0fdf4,stroke:#16a34a,stroke-width:1px
    style DOMAIN fill:#fffbeb,stroke:#d97706,stroke-width:1px
    style INFRA fill:#f5f3ff,stroke:#7c3aed,stroke-width:1px
    style USES fill:#ffffff,stroke:#86efac,stroke-width:1px
    style PORTS fill:#ffffff,stroke:#86efac,stroke-width:1px
    style ENT fill:#ffffff,stroke:#fbbf24,stroke-width:1px
```

## 4. Interpretación del diagrama

### Presentación

La capa **API** contiene los endpoints y mecanismos necesarios para recibir solicitudes, autenticar usuarios, aplicar autorización y validar datos de entrada. No contiene las reglas centrales del negocio.

### Application

La capa **Application** coordina los casos de uso del sistema. También define los contratos o puertos que necesita para acceder a persistencia, caché, auditoría e integraciones externas.

Entre los casos de uso representativos se encuentran:

- gestionar legajos;
- gestionar historia laboral;
- resolver solicitudes de actualización;
- generar reportes e indicadores.

### Domain

La capa **Domain** constituye el núcleo del negocio. Contiene entidades, conceptos y reglas relacionadas con trabajadores, legajos, vinculaciones laborales, contratos, documentos y solicitudes.

Esta capa no depende de ASP.NET Core, Entity Framework Core, PostgreSQL, Redis ni servicios externos.

### Infrastructure

La capa **Infrastructure** implementa los contratos definidos por Application. Incluye:

- persistencia mediante Entity Framework Core y PostgreSQL;
- acceso opcional a Redis;
- adaptadores para RENIEC y validación tributaria;
- implementaciones técnicas de auditoría y otros servicios de soporte.

### Raíz de composición

La configuración de **Dependency Injection** en ASP.NET Core registra qué implementación concreta satisface cada contrato. De esta manera, los casos de uso trabajan con abstracciones y no dependen directamente de tecnologías externas.

## 5. Leyenda

- **Flecha continua:** llamada o comunicación en tiempo de ejecución.
- **Flecha discontinua “depende de”:** dependencia hacia una abstracción.
- **Flecha discontinua “implementa”:** inversión de dependencias; Infrastructure implementa contratos definidos por Application.
- **Azul:** presentación.
- **Verde:** aplicación.
- **Amarillo:** dominio.
- **Morado:** infraestructura.
- **Gris:** tecnologías o sistemas externos.

## 6. Reglas de dependencia

1. **Domain** no depende de ninguna capa externa ni de frameworks.
2. **Application** depende de Domain y utiliza contratos para solicitar servicios externos.
3. **Infrastructure** implementa los contratos definidos por Application.
4. **API** invoca los casos de uso de Application y no accede directamente a PostgreSQL.
5. Los casos de uso no conocen implementaciones concretas de PostgreSQL, Redis, RENIEC ni otros servicios.
6. Cambiar una tecnología externa debe afectar principalmente Infrastructure y la configuración de dependencias, no las reglas del dominio.
