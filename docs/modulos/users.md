# Diseño del Módulo – Users

## Objetivo

Diseñar el módulo `users`, encargado de gestionar el perfil y datos personales del usuario, incluyendo operaciones de lectura, actualización y futuras funcionalidades como historial de actividad, imagen de perfil y configuración de cuenta.

---

## Estructura del módulo

```
/modules/users/
├── users.controller.ts
├── users.router.ts
├── users.service.ts
├── users.model.ts
├── users.validations.ts
├── dtos/
│   └── users.dto.ts
├── interfaces/
│   ├── IUser.ts
│   └── IUserModel.ts
└── index.ts
```

---

## Flujos principales

### Obtener un perfil 
1. Usuario autenticado accede a `GET /api/users/ejemplo`
2. Se responde con DTO del usuario

### Actualizar perfil
1. Usuario envía `PUT /api/users/me` con nuevos datos
2. Validaciones revisan que el nuevo correo, username o imagen sean válidos
3. Se actualiza entrada en base de datos
4. Se responde con datos actualizados

---

## Validaciones

- Username: único, sin espacios, 3–15 caracteres
- Email: formato válido, único
- Imagen de perfil: opcional, máximo 2MB
- Descripción o bio: máximo 300 caracteres

---

## Dependencias

- `auth`: obtiene ID del usuario desde JWT
- `posts`: para mostrar posts creados por el usuario
- `comments`: para listar actividad reciente
- `notifications`: para integrar panel de avisos personales

---

## Posibles tareas técnicas 

- [ ] Definir rutas REST:
  - `GET /api/users/me`
  - `PUT /api/users/me`
  - `GET /api/users/:id`
- [ ] DTOs para respuesta segura (sin contraseña ni tokens)
- [ ] Validaciones robustas
- [ ] Tests de integración
- [ ] Soporte para imagen de perfil y descripcion (opcional y futura)

---

## Notas

- El módulo está pensado para crecer con funciones sociales (seguimiento, favoritos, historial)
- Se puede integrar con `email` para notificaciones de cambios de cuenta o recuperación
- Es base para otras vistas como "perfil público", "actividad reciente" y "configuración de cuenta"

