# Diseño del Módulo – Comments

## Objetivo

Diseñar el módulo `comments`, responsable de la creación, visualización y gestión de comentarios en posts. Este módulo también se integra con notificaciones futuras y puede soportar moderación si se activa el rol administrador (también futuro).

---

## Estructura del módulo

```
/modules/comments/
├── comments.controller.ts
├── comments.router.ts
├── comments.service.ts
├── comments.model.ts         
├── comments.validations.ts
├── dto/
│   └── comments.dto.ts
├── interfaces/
│   └── ICommentsModel.ts
│   └── IComment.ts
└── index.ts
```

---

## Flujo principal: Crear comentario

1. Usuario autenticado accede a POST `/api/comments`
2. Middleware protege la ruta (JWT)
3. Validaciones revisan que el comentario tenga contenido, ID de post válido y autor válido
4. Se crea entrada en la base de datos (con timestamps)
5. Se puede emitir evento a sistema de notificaciones

---

## Validaciones

- Contenido (obligatorio, máximo 500 caracteres)
- ID de post (UUID válido, debe existir)
- Autor (obtenido desde JWT)
- No se permite spam repetido ni comentarios vacíos

---

## Dependencias

- `posts`: validar que el post al que se comenta existe
- `auth`: validar que el usuario esté logueado
- `notifications` (futuro): para avisar al autor del post

---

## Posibles tareas técnicas 

- [ ] Endpoints REST:
  - `POST /api/comments`
  - `GET /api/comments?postId=xyz`
  - `DELETE /api/comments/:id` (solo si autor o admin)
- [ ] Lógica de visibilidad (mostrar comentarios por post, ordenados por fecha)
- [ ] Validaciones con Zod/Yup
- [ ] Tests de integración (comentarios, errores comunes)
- [ ] Relación con `posts` y `users` en el modelo Prisma

---

## Notas

- El módulo puede crecer hacia respuestas en hilos o votación de comentarios
- El diseño actual permite extracción a microservicio si se quiere manejar alta frecuencia (con colas o buffers)
- Puede integrarse lógica de moderación automática si se detecta spam o lenguaje ofensivo en el futuro

