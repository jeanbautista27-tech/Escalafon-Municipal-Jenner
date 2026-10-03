# Arquitectura inicial del sistema

## Descripción

Se propone una aplicación web para gestionar la información escalafonaria del personal municipal. La solución tendrá un frontend web y un backend organizado como monolito modular con Clean Architecture.

## Componentes principales

- **Interfaz web:** React y TypeScript.
- **Balanceador de carga:** AWS Application Load Balancer.
- **API REST:** ASP.NET Core con .NET 8.
- **Backend:** capas API, Application, Domain e Infrastructure.
- **Persistencia:** PostgreSQL.
- **Caché:** Redis.
- **Ejecución de servicios:** Docker y Docker Compose.

## Diagrama de arquitectura inicial

```mermaid
flowchart TB
    USERS["Usuarios<br/>Administrador general<br/>Administrador de escalafón<br/>Trabajador municipal"]
    WEB["Interfaz web<br/>React + TypeScript"]
    ALB["AWS Application<br/>Load Balancer"]
    API["API REST<br/>ASP.NET Core / .NET 8"]

    subgraph BACKEND["Backend: monolito modular con Clean Architecture"]
        APP["Application<br/>Casos de uso"]
        DOMAIN["Domain<br/>Entidades y reglas de negocio"]
        INFRA["Infrastructure<br/>Persistencia y caché"]
        API --> APP
        APP --> DOMAIN
        INFRA -. "implementa interfaces" .-> APP
    end

    PG["PostgreSQL"]
    REDIS["Redis"]

    USERS --> WEB
    WEB --> ALB
    ALB --> API
    INFRA --> PG
    INFRA --> REDIS
```

## Flujo general

Los usuarios acceden al sistema desde la interfaz web. Esta se comunica con la API REST a través del balanceador de carga. La API coordina los casos de uso de Application, que aplican las reglas de Domain. Infrastructure conecta el backend con PostgreSQL y Redis.

La arquitectura inicial se enfoca en el sistema escalafonario y permitirá incorporar otros módulos gradualmente.