# Arquitectura inicial del sistema

## Diagrama de arquitectura

```mermaid
flowchart TD

%% =========================
%% ACTORES
%% =========================
subgraph ACTORES["ACTORES"]
    Admin["Administrador del Sistema"]
    Responsable["Responsable de Escalafón"]
    Trabajador["Trabajador municipal"]
    Consulta["Usuario de Consulta Interna / Gerencia"]
end

%% =========================
%% PRESENTACIÓN
%% =========================
subgraph PRESENTACION["PRESENTACIÓN"]
    Web["Aplicación Web<br/>React + TypeScript"]
    API["API REST<br/>ASP.NET Core / .NET 8"]
end

%% =========================
%% LÓGICA DE NEGOCIO
%% =========================
subgraph NEGOCIO["LÓGICA DE NEGOCIO"]
    Seguridad["Administración y Seguridad"]
    Legajos["Trabajadores y Legajos"]
    Laboral["Gestión Laboral e Historial"]
    Documentos["Documentos y Solicitudes"]
    Organizacion["Organización y Catálogos"]
    Reportes["Alertas, Dashboard y Reportes"]
    Migracion["Migración e Integraciones"]
end

%% =========================
%% DATOS
%% =========================
subgraph DATOS["DATOS"]
    PostgreSQL["PostgreSQL<br/>Fuente de verdad"]
    Redis["Redis<br/>Caché"]
end

%% =========================
%% SISTEMAS / FUENTES EXTERNAS
%% =========================
subgraph EXTERNOS["SISTEMAS Y FUENTES EXTERNAS"]
    Reniec["RENIEC<br/>Validación de identidad"]
    Tributaria["Servicio de validación tributaria<br/>cuando esté disponible"]
    Excel["Archivo Excel<br/>Migración inicial"]
end

%% =========================
%% FLUJO PRINCIPAL
%% =========================
ACTORES --> Web
Web --> API
API --> NEGOCIO
NEGOCIO --> PostgreSQL
NEGOCIO -. "uso opcional de caché" .-> Redis

%% =========================
%% INTEGRACIONES
%% =========================
Migracion -. "validación" .-> Reniec
Migracion -. "validación" .-> Tributaria
Excel --> Migracion

%% =========================
%% DISTRIBUCIÓN HORIZONTAL
%% =========================
Admin ~~~ Responsable
Responsable ~~~ Trabajador
Trabajador ~~~ Consulta

Seguridad ~~~ Legajos
Legajos ~~~ Laboral
Laboral ~~~ Documentos
Documentos ~~~ Organizacion
Organizacion ~~~ Reportes
Reportes ~~~ Migracion

Reniec ~~~ Tributaria
Tributaria ~~~ Excel

%% =========================
%% ESTILOS
%% =========================
style ACTORES fill:#222,stroke:#fff,stroke-width:2px,color:#fff
style PRESENTACION fill:#222,stroke:#fff,stroke-width:2px,color:#fff
style NEGOCIO fill:#222,stroke:#fff,stroke-width:2px,color:#fff
style DATOS fill:#222,stroke:#fff,stroke-width:2px,color:#fff
style EXTERNOS fill:#222,stroke:#fff,stroke-width:2px,color:#fff

style Admin fill:#222,stroke:#fff,color:#fff
style Responsable fill:#222,stroke:#fff,color:#fff
style Trabajador fill:#222,stroke:#fff,color:#fff
style Consulta fill:#222,stroke:#fff,color:#fff

style Web fill:#222,stroke:#fff,color:#fff
style API fill:#222,stroke:#fff,color:#fff

style Seguridad fill:#222,stroke:#fff,color:#fff
style Legajos fill:#222,stroke:#fff,color:#fff
style Laboral fill:#222,stroke:#fff,color:#fff
style Documentos fill:#222,stroke:#fff,color:#fff
style Organizacion fill:#222,stroke:#fff,color:#fff
style Reportes fill:#222,stroke:#fff,color:#fff
style Migracion fill:#222,stroke:#fff,color:#fff

style PostgreSQL fill:#222,stroke:#fff,color:#fff
style Redis fill:#222,stroke:#fff,color:#fff

style Reniec fill:#222,stroke:#fff,color:#fff
style Tributaria fill:#222,stroke:#fff,color:#fff
style Excel fill:#222,stroke:#fff,color:#fff
```

## Descripción

La arquitectura inicial del Sistema de Gestión Escalafonaria del Personal Municipal se organiza en presentación, lógica de negocio, datos e integraciones externas.

- **Actores:** participan el Administrador del Sistema, Responsable de Escalafón, Trabajador municipal y Usuario de Consulta Interna / Gerencia, cada uno con funciones y restricciones de acceso diferenciadas.
- **Presentación:** la interacción se realiza mediante una aplicación web desarrollada con React y TypeScript, que consume una API REST implementada con ASP.NET Core sobre .NET 8.
- **Lógica de negocio:** concentra las funcionalidades principales de administración y seguridad, trabajadores y legajos, gestión laboral e historial, documentos y solicitudes, organización y catálogos, alertas y reportes, además de migración e integraciones.
- **Datos:** PostgreSQL constituye la fuente de verdad de la información funcional e histórica. Redis se utiliza únicamente como apoyo para caché u optimización cuando sea necesario.
- **Integraciones externas:** RENIEC y el servicio de validación tributaria se consideran integraciones desacopladas y opcionales. La indisponibilidad de estos servicios no debe bloquear las operaciones principales del sistema.
- **Migración inicial:** la información existente en archivos Excel puede incorporarse mediante un proceso controlado de validación, previsualización y confirmación antes de persistirla en PostgreSQL.

La solución se implementa como un **monolito modular**, manteniendo la separación de responsabilidades definida por Clean Architecture.
