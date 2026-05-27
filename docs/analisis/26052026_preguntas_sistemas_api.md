# Preguntas preliminares para Sistemas — Contrato y criterios generales de API

## Objetivo

Consolidar criterios técnicos y funcionales generales antes de continuar el análisis masivo de endpoints de la API RANIE.

La finalidad de este documento es evitar asumir comportamientos, políticas de exposición o criterios arquitectónicos que puedan afectar la documentación posterior.

---

# Alcance

Este documento:

- NO propone cambios definitivos;
- NO representa decisiones acordadas;
- NO implica observaciones críticas sobre la implementación actual.

Su objetivo es alinear criterios institucionales y técnicos antes de documentar masivamente los recursos de la API.

---

# Lineamientos funcionales definidos por el área solicitante

El área solicitante establece preliminarmente los siguientes criterios funcionales:

| Tema | Lineamiento |
|---|---|
| Usuarios administrativos | Deben existir usuarios con capacidad de habilitar usuarios y permisos |
| Analistas | Deben existir usuarios autenticados con acceso a campos útiles definidos funcionalmente |
| Usuarios públicos | Deben existir endpoints o respuestas públicas sin token con información básica |
| Consumo | La API será utilizada inicialmente para consumo crudo |
| Aplicaciones | No se prevé inicialmente desarrollo de aplicaciones consumidoras oficiales |
| Documentación | La documentación debe ser pública y accesible |

Estos lineamientos representan necesidades funcionales preliminares del área solicitante y requieren validación técnica y arquitectónica por parte de Sistemas.

---

# Observaciones preliminares detectadas

Durante el análisis inicial del bloque `/edificios` se detectaron:

- diferencias entre `id` interno y `cui`;
- coexistencia de path params y filtros query;
- joins implícitos en respuestas;
- exposición de campos técnicos;
- filtros funcionales parcialmente documentados;
- diferencias entre Swagger y comportamiento real observado;
- dependencia obligatoria de Bearer Token;
- respuestas condicionadas por autenticación.

Estas observaciones motivan la necesidad de validar criterios generales antes de continuar con el relevamiento completo.

---

# Preguntas generales

## Identificadores

| Tema | Pregunta |
|---|---|
| `id` interno vs `cui` | ¿Cuál debe considerarse identificador principal a nivel API? |
| Path params | ¿`/edificios/{id}` debe documentarse explícitamente como ID interno? |
| CUI | ¿Conviene disponer de endpoint específico por CUI? |
| Identificadores públicos | ¿Qué identificadores son considerados seguros para exposición pública? |

---

# Contrato de endpoints

| Tema | Pregunta |
|---|---|
| Endpoint único | ¿Se espera que un mismo endpoint devuelva respuestas distintas según rol? |
| Endpoints separados | ¿Prefieren separar endpoints públicos, internos y administrativos? |
| Contrato funcional | ¿La API apunta a exposición cruda de tablas o a contratos funcionales? |
| Versionado | ¿Existe estrategia de versionado de API? |
| Compatibilidad | ¿Hay compromiso de backward compatibility? |

---

# Exposición de datos

| Tema | Pregunta |
|---|---|
| Campos técnicos | ¿Qué campos internos deberían ocultarse según perfil? |
| Auditoría | ¿`createdAt` y `updatedAt` deben exponerse? |
| Soft delete | ¿El campo `borrado` debe ser visible? |
| Relaciones | ¿Qué joins consideran válidos institucionalmente? |
| Geometrías | ¿La exposición de `geom` está prevista para consumo GIS? |
| Coordenadas | ¿Debe exponerse simultáneamente GKBA y WGS84? |
| Campos públicos | ¿Cómo se diferencian los campos básicos públicos de los campos útiles para analistas? |

---

# Swagger y documentación

| Tema | Pregunta |
|---|---|
| Swagger | ¿Swagger es considerado documentación oficial? |
| Mantenimiento | ¿Quién mantiene Swagger/documentación? |
| Filtros | ¿Todos los filtros soportados están documentados? |
| Descripciones | ¿Existe revisión funcional de textos y parámetros? |
| Seguridad | ¿Swagger debería indicar explícitamente autenticación requerida? |
| Ejemplos | ¿Existe criterio institucional para ejemplos de request/response? |
| Publicación | ¿La documentación será pública para terceros consumidores? |

---

# Permisos y autenticación

| Tema | Pregunta |
|---|---|
| Roles | ¿Los roles funcionales ya están definidos institucionalmente? |
| Filtrado por rol | ¿La API debería ocultar campos según perfil? |
| Endpoints públicos | ¿Qué recursos se espera publicar sin token? |
| Bearer/JWT | ¿Existe expiración y refresh token definidos? |
| Permisos | ¿Los permisos son endpoint-based o acción-based? |
| Testing | ¿Existen usuarios específicos para QA/documentación? |
| Superadmin | ¿Qué capacidades concretas tendrá el perfil administrador total? |

---

# Escritura y borrado

| Tema | Pregunta |
|---|---|
| `POST` | ¿Los endpoints de escritura ya impactan sobre base productiva? |
| `PATCH` | ¿Existen auditorías de modificaciones? |
| `DELETE` | ¿El borrado es lógico o físico? |
| Recuperación | ¿Puede revertirse un borrado? |
| Validaciones | ¿Las validaciones están centralizadas o endpoint por endpoint? |

---

# Ambientes

| Tema | Pregunta |
|---|---|
| `ranie-test` | ¿Corresponde efectivamente a testing? |
| Bases | ¿Existen ambientes separados? |
| Datos de prueba | ¿Hay registros descartables para testing? |
| Replicación | ¿Testing replica productivo? |
| Frecuencia | ¿Cada cuánto se sincronizan ambientes? |

---

# Paginación y performance

| Tema | Pregunta |
|---|---|
| Paginación | ¿Será obligatoria en todos los listados? |
| Límites | ¿Existen límites máximos de resultados? |
| Performance | ¿Hay criterios de optimización definidos? |
| Geometrías | ¿Existen límites especiales para respuestas geográficas? |
| Joins | ¿Hay restricciones institucionales sobre joins pesados? |

---

# Objetivo posterior

Una vez alineados estos criterios, continuar con:

- análisis detallado de endpoints;
- documentación funcional;
- clasificación de permisos;
- propuestas de mejora;
- definición de contratos consistentes;
- normalización documental de Swagger;
- definición de criterios de exposición pública.

---

# Estado del documento

Documento preliminar de alineación técnica.

No representa decisiones definitivas.