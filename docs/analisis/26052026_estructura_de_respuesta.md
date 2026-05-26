## Observación sobre estructura de respuestas

Actualmente algunos endpoints devuelven tablas completas. Se propone revisar, endpoint por endpoint, qué campos deben exponerse en el JSON y cuáles no, según perfil de usuario y finalidad del consumo.

Asimismo, sería útil evaluar la incorporación de endpoints de consulta compuesta o joineada, orientados al consumo funcional. Estos endpoints permitirían obtener en una única respuesta información integrada de varias tablas relacionadas, evitando que el cliente deba reconstruir relaciones del lado frontend o consumir múltiples endpoints para una misma consulta.