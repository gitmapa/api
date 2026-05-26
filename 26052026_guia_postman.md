# Guía básica de pruebas de API utilizando Postman

## Objetivo

Documentar un procedimiento básico para replicar pruebas sobre la API RANIE utilizando Postman.

La finalidad de esta guía es:

- facilitar pruebas manuales;
- documentar comportamiento observado;
- validar endpoints;
- analizar estructuras JSON;
- verificar autenticación;
- registrar respuestas de la API.

---

# Requisitos

## Software

| Herramienta | Descripción |
|---|---|
| Postman | Cliente para pruebas de APIs |
| Navegador web | Acceso a Swagger |
| Token Bearer/JWT | Requerido para endpoints protegidos |

---

# Documentación Swagger

La documentación interactiva se encuentra disponible en:

https://ranie-test.bue.edu.ar/api/docs/

Swagger permite:

- visualizar endpoints;
- ver parámetros;
- identificar métodos HTTP;
- observar ejemplos de request;
- probar requests simples.

Sin embargo, para análisis técnicos más completos se recomienda utilizar Postman.

---

# Configuración inicial de Postman

## Crear una colección

Se recomienda crear una colección llamada:

RANIE API

Dentro de la colección pueden agruparse carpetas por recurso:

- auth
- users
- edificios
- etc.

---

# Variables recomendadas

## Variable `base_url`

Crear una variable de colección:

| Variable | Valor sugerido |
|---|---|
| `base_url` | `https://ranie-test.bue.edu.ar/api` |

De esta manera los endpoints pueden escribirse como:

{{base_url}}/edificios

---

# Autenticación Bearer/JWT

## Obtener token

Utilizar el endpoint:

POST /auth/login

Con body tipo JSON.

Ejemplo general:

{
  "email": "usuario",
  "password": "contraseña"
}

---

## Configurar token en Postman

En la colección:

Authorization → Bearer Token

Pegar el JWT obtenido.

De esta forma todas las requests heredarán autenticación automáticamente.

---

# Información útil a registrar durante las pruebas

Para cada endpoint analizado se recomienda registrar:

| Elemento | Descripción |
|---|---|
| Endpoint | Ruta utilizada |
| Método HTTP | GET / POST / PATCH / DELETE |
| Headers | Especialmente Authorization |
| Query params | Parámetros enviados |
| Body | JSON enviado |
| Status code | Código HTTP devuelto |
| Tiempo de respuesta | Performance básica |
| Response JSON | Estructura observada |
| Errores | Mensajes y comportamiento |

---

# Endpoints sensibles

## Precaución

Los siguientes métodos pueden modificar información real:

| Método | Riesgo |
|---|---|
| POST | Crea registros |
| PATCH | Modifica registros |
| DELETE | Elimina registros |

Antes de ejecutar pruebas se recomienda verificar:

- si el entorno corresponde a testing o producción;
- si el usuario posee permisos reales de escritura;
- si existen registros de prueba disponibles.

---

# Recomendaciones de análisis

## Observar especialmente

| Tema | Preguntas sugeridas |
|---|---|
| Exposición de datos | ¿Devuelve campos innecesarios? |
| Paginación | ¿Devuelve demasiados registros? |
| Filtros | ¿Permite búsquedas útiles? |
| Seguridad | ¿Requiere autenticación? |
| Errores | ¿Responde correctamente? |
| Performance | ¿Hay respuestas lentas? |
| Integridad | ¿Valida correctamente los datos? |

---

# Exportación de colecciones

Postman permite exportar:

- colecciones;
- environments;
- requests;
- ejemplos de respuestas.

Esto facilita:

- reproducibilidad;
- documentación;
- trabajo colaborativo;
- versionado en Git.

---

# Estado del documento

Documento preliminar de metodología de pruebas.

No representa lineamientos definitivos de implementación institucional.
