# Vista Lógica del Sistema – Blog Técnico Personal

## Objetivo

Describir cómo está organizado el sistema en módulos y cómo se estructura la lógica del backend y frontend, siguiendo un enfoque modular basado en recursos y responsabilidades.

---

## Backend – Node.js + Express (MVC modular por entidad)

El backend sigue una arquitectura tipo MVC, con una estructura modular organizada por entidad (auth, users, posts, comments, etc.). Cada entidad contiene su propia lógica distribuida en:

- **Controllers:** manejan la lógica de negocio
- **Routers:** definen los endpoints
- **Models:** conectan con la base de datos (Prisma y MongoDB)
- **DTOs/Validations:** validan entradas del usuario

También existen capas adicionales para servicios transversales (`emails/`, `services/`, `errors/`, `utils/`), interfaces tipadas por entidad y configuraciones de conexión a base de datos (MySQL y MongoDB).

> Nota: el módulo `emails/`, aunque actualmente está acoplado al backend, se planea extraer como un microservicio independiente en otro contenedor Docker para su reutilización en múltiples proyectos.

### Ejemplo de estructura interna (entidad `posts`):
```
posts/
├── posts.controller.ts
├── posts.model.ts
├── posts.router.ts
├── posts.validations.ts
├── dto/
│   └── posts.dto.ts
```

### Comunicación entre módulos
- Módulos como `comments` dependen del `id` del usuario y del `id` del post para relacionarse
- Middlewares de autenticación (ej. `protected.middleware.ts`) protegen rutas sensibles
- `emails/` se comunica con `auth` para funciones como verificación de cuenta y recuperación de contraseña

---

## Frontend – React + TypeScript (estructura por dominio y función)

El frontend está en construcción, pero sigue una estructura clara inspirada en principios de separación por responsabilidad. La organización se basa en:

- **`/components/`** divididos por dominio: `auth`, `posts`, `comments`, `users`, `layout`, etc.
- **`/pages/`** como vistas principales del enrutador (React Router)
- **`/contexts/` y `/hooks/`** para lógica de estado y reutilización
- **`/services/`** para llamadas a la API
- **`/types/`** y `/utils/` para tipado y funciones auxiliares

### Ejemplo de flujo:
- `Post.tsx` (página) renderiza `PostDetail` (componente) y `CommentSection`
- `CommentSection` usa `commentService` para obtener los comentarios
- `AuthContext` determina si se puede comentar

---

## Conexiones clave entre módulos

- Los **comentarios** dependen tanto de la entidad `user` como de `post`
- Los **tokens JWT** se gestionan vía `auth` y son verificados por middlewares para acceder a `posts`, `comments`, etc.
- La **verificación por correo** se conecta entre `auth`, `emails` y `services`
- El **frontend** comunica con el backend vía API REST usando `services/*.ts` (axios o fetch)

---

## Notas

Esta vista lógica refleja una arquitectura **modular organizada por dominio funcional**, siguiendo un enfoque monolítico pero escalable. Permite extender con nuevos módulos sin romper la estructura general, y se alinea con patrones modernos de diseño para aplicaciones fullstack con separación clara entre capas.

Se contempla la futura transición de algunos módulos (como `emails`) hacia microservicios independientes para promover la reutilización y desacoplamiento.

