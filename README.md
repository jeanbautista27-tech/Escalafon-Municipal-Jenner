# Sistema de Gestión Escalafonaria Municipal

## Descripción

Proyecto académico del curso de Arquitectura de Software. Busca organizar la información escalafonaria del personal municipal y facilitar su consulta y gestión.

## Objetivo

Proponer una solución que centralice la información del personal municipal y apoye las labores de administración, consulta y generación de reportes.

## Alcance inicial

- Gestionar la ficha escalafonaria de los trabajadores.
- Permitir la administración de información del personal.
- Facilitar a cada trabajador la consulta de su propia información.
- Generar reportes estadísticos.
- Registrar capacitaciones y certificaciones.
- Considerar alertas relacionadas con la jubilación próxima.

## Arquitectura propuesta

La propuesta considera un backend con ASP.NET Core y .NET 8, organizado en capas; PostgreSQL para la persistencia de datos; Redis para caché; y Docker para la ejecución del entorno. React con TypeScript se contempla para el frontend.

## Documentación

- `analisis-de-sistema/`: actores, historias de usuario, requisitos, atributos de calidad y restricciones.
- `arquitectura/`: diseño arquitectónico inicial del sistema.

## Curso

Arquitectura de Software