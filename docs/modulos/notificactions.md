# Diseño del Módulo – Notifications

## Objetivo

Diseñar el módulo `notifications`, encargado de generar, almacenar y enviar notificaciones a los usuarios sobre eventos relevantes como nuevos comentarios en sus publicaciones, respuestas a sus comentarios, cambios en su cuenta, y posibles interacciones sociales futuras (seguidores, menciones, etc.).

El módulo está pensado para desacoplarse como microservicio en el futuro.

---

## Estructura del módulo (propuesta)
```
/modules/notifications/
├── notifications.controller.ts
├── notifications.router.ts
├── notifications.service.ts
├── notifications.model.ts
├── notifications.validations.ts
├── dtos/
│ └── notifications.dto.ts
├── interfaces/
│ └── INotification.ts
└── index.ts
```
---

## Flujos principales

### Crear notificación al recibir comentario
1. Usuario A comenta un post de usuario B
2. `comments` llama a `notifications.service.create()`
3. Se guarda notificación con tipo `"new_comment"`, ID de post y de usuarios
4. Se actualiza lista de notificaciones no leídas de usuario B

### Consultar notificaciones
1. Usuario abre su panel (`GET /api/notifications`)
2. Se obtiene lista paginada de notificaciones más recientes
3. Usuario puede marcar como leídas o eliminar

---

## Validaciones

- Tipo de notificación permitido (`"new_comment"`, `"reply"`, `"account_change"`, etc.)
- Texto o metadatos con longitud limitada
- Destinatario debe existir
- Notificación no debe duplicarse si ya existe una activa del mismo tipo en ventana de tiempo corta

---

## Dependencias

- `users`: para obtener datos del destinatario
- `comments`, `posts`, `auth`: para disparar eventos
- `services/cache`: opcional para colas o temporizadores
- `email`: si se desea reenviar notificación por correo

---

## Posibles tareas técnicas 

- [ ] Modelo `Notification` en Prisma con campos: id, type, message, isRead, createdAt, userId, meta (JSON)
- [ ] Endpoints REST:
  - `GET /api/notifications` (listar)
  - `PATCH /api/notifications/:id/read` (marcar como leída)
  - `DELETE /api/notifications/:id` (eliminar)
- [ ] Middleware para autenticar rutas
- [ ] DTOs limpios para respuesta
- [ ] Interface del modelo y del modulo `Notification`
- [ ] Tests de integración

---

## Notas

- Puede incluir una mini UI en el frontend (ícono de campana con contador)
- Se puede extender para usar WebSockets en tiempo real
- Idealmente migrará a microservicio que consuma eventos de Kafka o RabbitMQ
- Puede añadirse una vista en el perfil del usuario con historial de notificaciones
