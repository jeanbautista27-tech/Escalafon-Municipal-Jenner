# Restricciones

Identificar las restricciones que condicionan las decisiones de diseño y arquitectura del Sistema de Gestión Escalafonaria del Personal Municipal.

| IDENTIFICACIÓN | Restricción | Descripción |
|---|---|---|
| RC01 | Aplicación web | El sistema debe desarrollarse como una aplicación web responsiva accesible mediante un navegador web. |
| RC02 | Control de versiones | El código fuente y la documentación del proyecto deben gestionarse utilizando Git y mantenerse en un repositorio de GitHub. |
| RC03 | API REST | La comunicación entre el frontend y el backend debe realizarse mediante una API REST. |
| RC04 | Alcance escalafonario | La primera versión debe centrarse exclusivamente en la gestión escalafonaria del personal municipal. No debe incluir planillas, remuneraciones, asistencia, presupuesto, tesorería ni cálculo de beneficios laborales. |
| RC05 | Gestión documental limitada | El sistema debe gestionar únicamente documentos sustentatorios relacionados con el legajo escalafonario. No debe implementar mesa de partes, trámite documentario general, correspondencia institucional, OCR avanzado ni firma digital institucional en esta versión. |
