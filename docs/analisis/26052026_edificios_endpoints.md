# Análisis inicial — Endpoints `/edificios`

## Objetivo

Analizar el comportamiento observado de los endpoints vinculados a edificios/CUI, considerando autenticación, estructura de respuestas, filtros, joins y exposición de datos.

El presente documento representa un análisis preliminar y no implica decisiones definitivas de implementación.

---

# Endpoints analizados

| Endpoint | Método | Descripción Swagger |
|---|---|---|
| `/edificios` | GET | Obtener todos los CUI |
| `/edificios/{id}` | GET | Obtener detalles de un CUI |
| `/edificios/cuinext` | GET | Obtener el siguiente CUI disponible |
| `/edificios` | POST | Crear un nuevo CUI |
| `/edificios/{id}` | PATCH | Actualiza un Edificios |
| `/edificios/{id}` | DELETE | Elimina un Edificios |

---

# Observaciones generales

El bloque `/edificios` representa uno de los recursos centrales de la API.

Se observan características de:

- paginación;
- filtros;
- joins implícitos;
- serialización geográfica;
- autenticación Bearer/JWT;
- respuestas orientadas a consumo funcional.

---

# Observación sobre autenticación

## Resultado observado

| Endpoint | Sin token | Con token |
|---|---|---|
| `GET /edificios` | `401 Unauthorized` | `200 OK` |
| `GET /edificios/{id}` | `401 Unauthorized` | `200 OK` |

Por lo observado, los endpoints analizados requieren autenticación Bearer/JWT.

---

# Observación sobre identificadores

## Ambigüedad detectada entre `id` y `cui`

En la respuesta observada:

| Campo | Valor observado |
|---|---|
| `id` | `975` |
| `cui` | `200984` |

Esto sugiere que:

| Endpoint | Utiliza |
|---|---|
| `/edificios/{id}` | ID interno |
| `/edificios?cui=` | CUI institucional |

Actualmente Swagger describe `GET /edificios/{id}` como:

```text
Obtener detalles de un CUI
```

Sin embargo, el parámetro utilizado corresponde aparentemente al identificador interno de base y no al CUI institucional.

---

# Análisis — `GET /edificios/{id}`

## Request observada

```text
GET /edificios/975
```

## Resultado observado

| Aspecto | Valor |
|---|---|
| Status code | `200 OK` |
| Tiempo de respuesta | `497 ms` |
| Tipo de respuesta | Objeto único |
| Requiere token | Sí |

---

# Campos observados en respuesta

| Campo | Observación preliminar |
|---|---|
| `createdAt` | Campo técnico/auditoría |
| `updatedAt` | Campo técnico/auditoría |
| `id` | Identificador interno |
| `cui` | Identificador institucional |
| `sector` | Campo funcional útil |
| `x_gkba`, `y_gkba` | Coordenadas locales |
| `x_wgs84`, `y_wgs84` | Coordenadas WGS84 |
| `geom` | Geometría serializada |
| `gestionado` | Campo funcional |
| `institucion` | Actualmente `null` |
| `borrado` | Campo interno |
| `tipoEstado` | Relación joineada |
| `predio` | Actualmente `null` |

---

# Observaciones sobre joins

El endpoint devuelve relaciones embebidas como:

| Relación | Observación |
|---|---|
| `tipoEstado` | Joineado automáticamente |
| `predio` | Relación prevista pero vacía |

Esto sugiere que la API ya implementa cierto nivel de resolución funcional y no únicamente exposición directa de tablas.

---

# Observaciones sobre exposición de datos

Actualmente algunos objetos relacionados devuelven campos técnicos posiblemente innecesarios para ciertos perfiles.

Ejemplo:

| Objeto | Campo posiblemente innecesario |
|---|---|
| `tipoEstado` | `createdAt` |
| `tipoEstado` | `updatedAt` |

---

# Análisis — `GET /edificios`

## Parámetros observados en Swagger

| Parámetro | Tipo | Descripción Swagger |
|---|---|---|
| `page` | number | Número de página |
| `limit` | number | Cantidad de resultados por página |
| `sort` | string | Orden ascendente/descendente |
| `cui` | number | Filtrar por ID de operativo |
| `altura` | number | Filtrar por altura |
| `calle` | string | Calle de la dirección |

---

# Observaciones sobre filtros

El endpoint soporta:

- paginación;
- ordenamiento;
- búsqueda por CUI;
- búsqueda por dirección.

Esto indica una orientación funcional del endpoint más allá de un simple listado de registros.

---

# Observaciones documentales

## Inconsistencias detectadas

| Elemento | Observación |
|---|---|
| `/edificios/{id}` | Swagger habla de CUI pero utiliza ID interno |
| parámetro `cui` | Descripto como “ID de operativo” |
| descripción general | “Obtener todos los CUI” resulta insuficiente |

---

# Observaciones sobre consumo GIS

La respuesta incluye:

- coordenadas GKBA;
- coordenadas WGS84;
- objeto `geom`.

Esto facilita integración futura con:

- clientes SIG;
- mapas web;
- servicios geográficos;
- análisis espaciales.

---

# Roles preliminares considerados

| Rol | Lectura | Escritura | Borrado |
|---|---|---|---|
| Público | Parcial/restringida | No | No |
| Analista | Sí | No |
| Admin | Sí | Parcial |
| Superadmin | Total | Sí | Sí |

---

# Estado del documento

Documento preliminar de análisis técnico y funcional.

No representa decisiones definitivas de implementación.
