# Arquitectura inicial del sistema

## Diagrama de arquitectura

```mermaid
flowchart TD
    subgraph ACT["ACTORES"]
        direction LR
        AG["Administrador general"] ~~~ AE["Administrador de escalafón"] ~~~ TR["Trabajador municipal"]
    end

    subgraph PRES["PRESENTACIÓN"]
        WEB["Aplicación web<br/>React + TypeScript"]
    end

    LB["AWS Application Load Balancer"]
    API["API REST<br/>ASP.NET Core / .NET 8"]

    subgraph NEG["LÓGICA DE NEGOCIO"]
        direction LR
        US["Usuarios y roles"] ~~~ ESC["Escalafón"] ~~~ PLA["Plazas y áreas"] ~~~ CAP["Capacitaciones"] ~~~ REP["Reportes y alertas"]
    end

    subgraph DAT["DATOS"]
        direction LR
        PG["PostgreSQL"] ~~~ RED["Redis<br/>Caché"]
    end

    subgraph EXT["INTEGRACIONES FUTURAS"]
        OTROS["Otros módulos institucionales<br/>(por definir)"]
    end

    ACT --> PRES
    PRES --> LB
    LB --> API
    API --> NEG
    NEG --> DAT
    API -. "cuando se definan" .-> OTROS

    classDef dark fill:#222,stroke:#fff,color:#fff
    class AG,AE,TR,WEB,LB,API,US,ESC,PLA,CAP,REP,PG,RED,OTROS dark
    style ACT fill:#222,stroke:#fff,color:#fff
    style PRES fill:#222,stroke:#fff,color:#fff
    style NEG fill:#222,stroke:#fff,color:#fff
    style DAT fill:#222,stroke:#fff,color:#fff
    style EXT fill:#222,stroke:#fff,color:#fff
```

## Descripción

La arquitectura inicial organiza el sistema en presentación, lógica de negocio y datos. La interfaz web se comunica con el backend mediante una API REST. El backend se desarrollará con ASP.NET Core y .NET 8, como un monolito modular organizado con Clean Architecture.

- **Presentación:** permite que los usuarios interactúen con el sistema desde una aplicación web.
- **Lógica de negocio:** reúne los módulos de usuarios y roles, escalafón, plazas y áreas, capacitaciones, reportes y alertas.
- **Datos:** PostgreSQL almacena la información y Redis se considera para las funciones de caché.
- **Balanceo:** AWS Application Load Balancer distribuye las solicitudes hacia el backend.
- **Integraciones futuras:** se incorporarán gradualmente cuando se definan los módulos institucionales correspondientes.