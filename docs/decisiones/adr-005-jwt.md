# ADR 005 – Uso de JWT (JSON Web Tokens) para autenticación

## Contexto

El sistema requiere un mecanismo de autenticación para identificar a los usuarios y proteger rutas privadas del backend. Para mantener el backend sin estado (stateless) y facilitar la escalabilidad, se optó por utilizar JWT (JSON Web Tokens) en lugar de sesiones almacenadas en servidor o cookies persistentes.

Una de las razones principales para elegir JWT fue evitar tener sesiones almacenadas en base de datos, lo que reduce la carga del backend y mejora la seguridad general. Además, se utilizan dos tipos de JWT:

- Un **token de sesión** con duración corta
- Un **refresh token** con duración más larga para renovar la sesión automáticamente

Ambos se guardan en cookies para evitar exposición directa al cliente. En el `localStorage` solo se guarda el `id` y el `nombre` del usuario, sin incluir ningún token.

Está previsto permitir invalidar o revocar tokens, por ejemplo, en caso de recuperación de cuenta, solicitud de cierre de sesión en todos los dispositivos o detección de robo de token. Esto permitiría bloquear a un usuario específico o invalidar su refresh token.

## Decisión

Se implementó JWT como método principal de autenticación. Los tokens son generados en el backend tras un login exitoso, y enviados al frontend dentro de cookies seguras. Cada solicitud a rutas protegidas debe incluir el token de sesión automáticamente desde las cookies. El backend valida el token en cada petición mediante middleware.

## Consecuencias

- ✅ Autenticación sin estado, ideal para APIs REST
- ✅ Fácil de integrar con middleware en Express
- ✅ Escalable a múltiples instancias del backend sin necesidad de sincronizar sesiones
- ✅ Uso de cookies y refresh token mejora la seguridad
- ⚠️ Requiere expiración controlada y estrategia para revocar tokens
- ⚠️ Aumenta la complejidad de gestión de sesiones (múltiples tokens, rutas de renovación)
- ⚠️ En caso de robo del refresh token, se necesitará una estrategia para invalidarlo por usuario

## Estado

Aceptado – 23 de junio de 2025

