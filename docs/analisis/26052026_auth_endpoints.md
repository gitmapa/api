# Análisis inicial — Endpoints de autenticación (`auth`)

## Objetivo

Documentar el comportamiento observado de los endpoints vinculados al proceso de autenticación, recuperación de contraseña y login federado mediante Google OAuth2.

El presente documento representa un análisis preliminar y no implica decisiones definitivas de implementación.

---

# Endpoints analizados

| Endpoint | Método | Descripción general |
|---|---|---|
| `/auth/login` | POST | Login mediante credenciales |
| `/auth/profile` | GET | Obtiene información del usuario autenticado |
| `/auth/google` | GET | Inicia autenticación OAuth2 con Google |
| `/auth/google/redirect` | GET | Callback de autenticación Google OAuth2 |
| `/auth/request-password-reset` | POST | Solicita recuperación de contraseña |
| `/auth/reset-password` | POST | Cambia contraseña utilizando token |

---

# Observaciones generales

El bloque `auth` concentra funcionalidades críticas vinculadas a:

- autenticación;
- emisión y validación de sesión;
- recuperación de acceso;
- integración con proveedor externo OAuth2;
- obtención del perfil autenticado.

Se recomienda considerar este conjunto de endpoints como superficie sensible de seguridad y documentar especialmente:

- expiración de tokens;
- formato del JWT;
- scopes/permisos;
- validación de sesiones;
- protección anti abuso;
- manejo de intentos fallidos;
- trazabilidad de login;
- expiración y reutilización de tokens de reseteo.

---

# Análisis por endpoint

## `POST /auth/login`

### Función

Permite autenticar un usuario utilizando credenciales locales.

### Observaciones

| Aspecto | Observación |
|---|---|
| Sensibilidad | Endpoint crítico |
| Exposición | Público |
| Requiere rate limiting | Sí |
| Generación de JWT | Probable |
| Riesgo principal | Fuerza bruta y enumeración de usuarios |

### Consideraciones sugeridas

- limitar intentos por IP;
- evitar mensajes distintos entre “usuario inexistente” y “contraseña incorrecta”;
- registrar auditoría de login;
- definir expiración de token;
- evaluar refresh token si la API escala.

---

## `GET /auth/profile`

### Función

Obtiene información del usuario autenticado a partir del token activo.

### Observaciones

| Aspecto | Observación |
|---|---|
| Acceso | Usuario autenticado |
| Utilidad frontend | Alta |
| Riesgo | Exposición excesiva de campos |

### Consideraciones sugeridas

Se recomienda que este endpoint exponga únicamente:

- identificador;
- nombre;
- email;
- rol;
- permisos necesarios para frontend.

Evitar devolver:

- hashes;
- tokens;
- información interna de autenticación;
- timestamps innecesarios;
- relaciones completas.

---

## `GET /auth/google`

### Función

Inicia flujo OAuth2 mediante autenticación Google.

### Observaciones

| Aspecto | Observación |
|---|---|
| Acceso | Público |
| Tipo | Redirección OAuth |
| Dependencia externa | Google |

### Consideraciones sugeridas

- validar dominios permitidos si corresponde;
- documentar claramente callback y flujo;
- definir comportamiento ante usuarios inexistentes;
- evaluar autoaprovisionamiento de usuarios.

---

## `GET /auth/google/redirect`

### Función

Procesa el callback OAuth2 luego de autenticación en Google.

### Observaciones

| Aspecto | Observación |
|---|---|
| Sensibilidad | Alta |
| Dependencia | OAuth2 |
| Riesgo | Validación incorrecta del callback |

### Consideraciones sugeridas

- validar `state`;
- validar tokens recibidos;
- registrar origen de autenticación;
- controlar asociación de cuentas duplicadas;
- evitar creación automática no controlada de usuarios.

---

## `POST /auth/request-password-reset`

### Función

Solicita recuperación de contraseña mediante token temporal.

### Observaciones

| Aspecto | Observación |
|---|---|
| Acceso | Público |
| Riesgo principal | Enumeración de usuarios |

### Consideraciones sugeridas

- responder siempre mensaje genérico;
- limitar frecuencia de solicitudes;
- registrar auditoría;
- definir expiración corta del token;
- invalidar solicitudes anteriores.

---

## `POST /auth/reset-password`

### Función

Permite modificar contraseña utilizando token de recuperación.

### Observaciones

| Aspecto | Observación |
|---|---|
| Sensibilidad | Crítica |
| Requiere token válido | Sí |
| Riesgo principal | Reutilización de token |

### Consideraciones sugeridas

- invalidar token luego del uso;
- definir expiración breve;
- exigir contraseña robusta;
- registrar auditoría de cambio;
- invalidar sesiones activas previas si corresponde.

---

# Observaciones funcionales

## Posible diferenciación futura de autenticación

A futuro podría evaluarse separar:

| Tipo | Objetivo |
|---|---|
| Auth interna | Usuarios administrativos |
| Auth pública | Usuarios externos |
| OAuth institucional | Integración SSO |
| API Tokens | Integraciones sistema-sistema |

---

# Riesgos técnicos generales observados

| Riesgo | Impacto |
|---|---|
| Exposición excesiva del perfil | Medio |
| Tokens sin expiración clara | Alto |
| Recuperación de contraseña sin límites | Alto |
| OAuth2 sin validaciones completas | Alto |
| Falta de auditoría | Medio |

---

# Recomendaciones preliminares

| Tema | Recomendación |
|---|---|
| Seguridad | Incorporar rate limiting |
| Auditoría | Registrar eventos críticos |
| JWT | Documentar expiración y claims |
| OAuth2 | Documentar flujo completo |
| Password reset | Invalidación inmediata de tokens |
| Frontend | Minimizar datos expuestos en `/profile` |

---

# Estado del documento

Documento preliminar de análisis técnico.

No representa decisiones definitivas de implementación.