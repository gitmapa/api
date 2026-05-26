# Preguntas preliminares para Sistemas — Contrato y criterios generales de API

## Objetivo

Consolidar criterios técnicos y funcionales generales antes de continuar el análisis masivo de endpoints de la API.

La finalidad de este documento es evitar asumir comportamientos, políticas de exposición o criterios arquitectónicos que puedan afectar la documentación posterior.

---

# Contexto

Durante el análisis preliminar del bloque `/edificios` se detectaron:

- diferencias entre `id` interno y `cui`;
- filtros funcionales no completamente documentados;
- joins implícitos;
- exposición de campos técnicos;
- ambigüedades documentales en Swagger.

Por este motivo se considera conveniente validar criterios generales antes de continuar con el análisis del resto de los recursos.

---

# Preguntas generales

## Identificadores

| Tema | Pregunta |
|---|---|
| `id` interno vs `cui` | ¿Cuál debe considerarse identificador principal a nivel API? |
| Path params | ¿`/edificios/{id}` debe documentarse explícitamente como ID interno? |
| CUI | ¿Conviene disponer de endpoint específico por CUI? |

---

# Contrato de endpoints

| Tema | Pregunta |
|---|---|
| Endpoint único | ¿Se espera que un mismo endpoint devuelva respuestas distintas según rol? |
| Endpoints separados | ¿Prefieren separar endpoints públicos, internos y administrativos? |
| Contrato funcional | ¿La API apunta a exposición cruda de tablas o a contratos funcionales? |

---

# Exposición de datos

| Tema | Pregunta |
|---|---|
| Campos técnicos | ¿Qué campos internos deberían ocultarse según perfil? |
| Auditoría | ¿`createdAt` y `updatedAt` deben exponerse? |
| Soft delete | ¿El campo `borrado` debe ser visible? |
| Relaciones | ¿Qué joins consideran válidos institucionalmente? |

---

# Swagger y documentación

| Tema | Pregunta |
|---|---|
| Swagger | ¿Swagger es considerado documentación oficial? |
| Mantenimiento | ¿Quién mantiene Swagger/documentación? |
| Filtros | ¿Todos los filtros soportados están documentados? |
| Descripciones | ¿Existe revisión funcional de textos y parámetros? |

---

# Permisos y autenticación

| Tema | Pregunta |
|---|---|
| Roles | ¿Los roles actuales son definitivos? |
| Filtrado por rol | ¿La API debería ocultar campos según perfil? |
| Endpoints públicos | ¿Qué recursos se espera publicar sin token? |
| Bearer/JWT | ¿Existe expiración y refresh token definidos? |

---

# Escritura y borrado

| Tema | Pregunta |
|---|---|
| `POST` | ¿Los endpoints de escritura ya impactan sobre base productiva? |
| `PATCH` | ¿Existen auditorías de modificaciones? |
| `DELETE` | ¿El borrado es lógico o físico? |
| Recuperación | ¿Puede revertirse un borrado? |

---

# Ambientes

| Tema | Pregunta |
|---|---|
| `ranie-test` | ¿Corresponde efectivamente a testing? |
| Bases | ¿Existen ambientes separados? |
| Datos de prueba | ¿Hay registros descartables para testing? |

---

# Paginación y performance

| Tema | Pregunta |
|---|---|
| Paginación | ¿Será obligatoria en todos los listados? |
| Límites | ¿Existen límites máximos de resultados? |
| Performance | ¿Hay criterios de optimización definidos? |

---

# Joins y consumo funcional

| Tema | Pregunta |
|---|---|
| Joins | ¿Qué relaciones deberían resolverse backend? |
| Frontend | ¿Qué relaciones esperan resolver desde frontend? |
| GIS | ¿La serialización geográfica es parte oficial del contrato API? |

---

# Objetivo posterior

Una vez alineados estos criterios, continuar con:

- análisis detallado de endpoints;
- documentación funcional;
- clasificación de permisos;
- propuestas de mejora;
- definición de contratos consistentes.

---

# Estado del documento

Documento preliminar de alineación técnica.

No representa decisiones definitivas.
