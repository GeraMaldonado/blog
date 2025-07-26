# Vista Dinámica – Flujo de creación de comentario

## Objetivo

Describir paso a paso cómo fluye la creación de un comentario en el sistema, desde el frontend hasta el backend, incluyendo validaciones, autenticación y respuesta al usuario.

---

## Escenario: Crear un comentario en un post

### 1. Interacción inicial en el frontend
- El usuario visualiza un post en `Post.tsx`
- El componente `CommentSection.tsx` muestra el formulario de comentario (`CommentForm.tsx`)
- El formulario requiere que el usuario esté autenticado (verificado vía `AuthContext`)
- Se realiza validación básica: texto no vacío, existencia de `userId` y `postId`

### 2. Envío al backend (API)
- El frontend llama a `commentService.createComment()`
- Se envía una petición `POST /api/comments` con los headers:
  - `Authorization: Bearer <token>`
  - Cuerpo JSON con `userId`, `postId`, y `content`

### 3. Middleware de autenticación
- El backend recibe la solicitud y la ruta pasa por `protected.middleware.ts`
- Se verifica la validez del JWT
  - Si no es válido y existe refresh token, se intenta renovar
  - Si ambos fallan, el backend responde con `401 Unauthorized`
  - El frontend limpia cookies y localStorage si ocurre este error

### 4. Validación y lógica del controlador
- El `comments.controller.ts` valida que:
  - El usuario existe en la base de datos
  - El post al que se comenta existe
  - El contenido cumple con reglas básicas
- Si todo es válido, se crea el comentario en base de datos (Prisma)

### 5. Respuesta al cliente
- El backend responde con:
  ```json
  {
    "status": "success",
    "comment": { ...nuevo comentario... }
  }
  ```
- El frontend actualiza la interfaz mostrando el nuevo comentario en `CommentList.tsx`

---

## Consideraciones de seguridad
- El token se almacena en cookies (no en localStorage)
- Solo el `userId` y `username` se almacenan en localStorage
- En caso de errores repetidos, el usuario es bloqueado temporalmente

---

## Notas
Este flujo refleja una separación clara de responsabilidades:
- Validaciones preliminares en el frontend
- Verificación de sesión con JWT y refresh tokens
- Validaciones de existencia en backend antes de insertar
- Retroalimentación inmediata al usuario sin recargar página

Esta vista puede ampliarse para incluir errores en red, recuperación de sesión, o integración con un sistema de notificaciones posterior.

