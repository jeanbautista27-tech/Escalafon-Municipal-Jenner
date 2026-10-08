cat > arquitectura/estilo-arquitectonico.md <<'EOF'
# Estilo arquitectónico

## 1. Sistema

**Sistema de Gestión Escalafonaria del Personal Municipal**

## 2. Estilo seleccionado

Se propone un **monolito modular**. El backend se organiza en módulos funcionales independientes dentro de una aplicación desplegable. Esta organización facilita el mantenimiento y permite ampliar el sistema gradualmente.

El sistema sigue también el modelo **cliente-servidor**: los usuarios acceden desde una interfaz web, que se comunica con el backend mediante una API REST.

## 3. Justificación

El monolito modular permite mantener organizados los módulos municipales y desplegar inicialmente la solución como una aplicación backend. También considera el crecimiento previsto del sistema, el requisito de atender al menos 1000 usuarios y la posibilidad de escalar horizontalmente mediante un balanceador de carga.

Las integraciones con otros sistemas institucionales se incorporarán gradualmente, según las necesidades que se definan.

## 4. Tecnologías y componentes principales

- **Interfaz web:** React y TypeScript.
- **API REST y backend:** ASP.NET Core y .NET 8.
- **Base de datos:** PostgreSQL.
- **Caché:** Redis.
- **Contenedores:** Docker y Docker Compose.
- **Balanceador previsto para el despliegue:** AWS Application Load Balancer.

## 5. Módulos funcionales considerados

- Usuarios y roles.
- Gestión de trabajadores.
- Ficha e historial escalafonario.
- Plazas y áreas.
- Capacitaciones.
- Reportes y alertas.
- Documentos y auditoría.

## 6. Diagrama de arquitectura global

```mermaid
flowchart TB
    subgraph actores["Usuarios del sistema"]
        direction LR
        admin["Administrador general"]
        escalafon["Administrador de escalafón"]
        trabajador["Trabajador municipal"]
    end

    cliente["Cliente web<br/>React + TypeScript"]
    balanceador["AWS Application Load Balancer<br/>despliegue previsto"]
    middleware["Backend ASP.NET Core / .NET 8<br/>Middlewares: CORS, autorización,<br/>validación, errores y logging"]

    admin --> cliente
    escalafon --> cliente
    trabajador --> cliente
    cliente -->|"HTTPS / JSON / REST"| balanceador
    balanceador --> middleware

    subgraph backend["Monolito modular del Sistema Escalafonario"]
        direction TB

        subgraph presentacion["1. Capa de presentación"]
            direction LR
            pUsuarios["Usuarios y roles<br/>Endpoints"]
            pPersonal["Trabajadores y escalafón<br/>Endpoints"]
            pPlazas["Plazas y capacitaciones<br/>Endpoints"]
            pReportes["Reportes y alertas<br/>Endpoints"]
        end

        subgraph aplicacion["2. Capa de lógica de negocio"]
            direction LR
            aUsuarios["Casos de uso<br/>Usuarios y trabajadores"]
            aEscalafon["Casos de uso<br/>Ficha e historial escalafonario"]
            aPlazas["Casos de uso<br/>Plazas y capacitaciones"]
            aReportes["Casos de uso<br/>Reportes y alertas"]
        end

        subgraph datos["3. Capa de datos e infraestructura"]
            direction LR
            repositorios["Repositorios<br/>Entity Framework Core"]
            cache["Caché<br/>Redis"]
            adaptadores["Adaptadores<br/>Integraciones futuras"]
        end

        pUsuarios --> aUsuarios
        pPersonal --> aEscalafon
        pPlazas --> aPlazas
        pReportes --> aReportes

        aUsuarios --> repositorios
        aEscalafon --> repositorios
        aPlazas --> repositorios
        aReportes --> repositorios
        aReportes -.-> cache
        aUsuarios -.-> adaptadores
    end

    middleware --> pUsuarios
    middleware --> pPersonal
    middleware --> pPlazas
    middleware --> pReportes

    postgres[("PostgreSQL")]
    sistemas["Sistemas institucionales<br/>integraciones futuras"]

    repositorios --> postgres
    adaptadores -.-> sistemas