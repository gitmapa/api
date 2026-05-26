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

    docs/
    ├── analisis/
    ├── endpoints/
    ├── propuestas/
    ├── decisiones/
    └── roadmap/

## Criterios de organización

| Carpeta | Uso previsto |
|---|---|
| `docs/analisis/` | Observaciones técnicas, revisiones preliminares y análisis funcionales. |
| `docs/endpoints/` | Documentación funcional por recurso o grupo de endpoints. |
| `docs/propuestas/` | Propuestas concretas de mejora o evolución. |
| `docs/decisiones/` | Criterios adoptados como referencia del proyecto. |
| `docs/roadmap/` | Planificación de evolución del trabajo. |

## Documentos iniciales

| Documento | Descripción |
|---|---|
| `docs/analisis/26052026_permisos.md` | Observaciones iniciales sobre roles, permisos y endpoints de usuarios. |
| `docs/analisis/26052026_estructura_de_respuesta.md` | Observaciones sobre exposición de campos y estructura de respuestas JSON. |
| `docs/analisis/26052026_auth_endpoints.md` | Análisis preliminar del bloque de autenticación. |
| `docs/analisis/26052026_guia_postman.md` | Guía básica para replicar pruebas de API con Postman. |

## Criterios generales de análisis

Los documentos del repositorio deben distinguir entre:

- comportamiento actual observado;
- problemas o riesgos detectados;
- comportamiento esperado;
- propuestas de mejora;
- decisiones adoptadas.

## Estado del repositorio

Repositorio en construcción.

La documentación incluida es preliminar y se irá ampliando a medida que se analicen nuevos endpoints y se registren resultados de pruebas.
