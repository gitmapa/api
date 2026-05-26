# API

Repositorio de análisis, documentación y observaciones técnicas vinculadas a la API RANIE.

## Objetivo

Centralizar documentación técnica, análisis funcionales, observaciones sobre endpoints, propuestas de mejora y criterios de acceso vinculados a la API institucional.

La finalidad de este repositorio es facilitar:

- comprensión de la estructura actual de la API;
- pruebas y consumo desde clientes externos;
- documentación de endpoints;
- análisis de seguridad y permisos;
- propuestas de evolución funcional;
- trazabilidad de decisiones técnicas.

## Documentación Swagger

Documentación interactiva disponible en:

https://ranie-test.bue.edu.ar/api/docs/

## Alcance actual

Actualmente el repositorio documenta y analiza:

- autenticación Bearer/JWT;
- endpoints de edificios;
- endpoints de usuarios;
- estructura general de respuestas JSON;
- criterios preliminares de permisos;
- observaciones sobre exposición de datos;
- posibilidades de endpoints joineados;
- consumo desde Postman.

## Estructura del repositorio

```text
docs/
├── analisis/
├── endpoints/
├── propuestas/
├── decisiones/
└── roadmap/