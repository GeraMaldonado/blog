# Funcionalidad Primaria – Blog Técnico Personal

## 1. Tipos de Usuario

- **Invitado / Lector anónimo / Visitante:** Puede navegar por el sitio, leer publicaciones, ver comentarios y perfiles públicos de usuarios registrados. No puede interactuar (comentar, seguir, crear contenido).

- **Usuario registrado:** Tiene una cuenta con autenticación. Puede:
  - Crear, editar y eliminar (lógicamente) sus propias publicaciones
  - Comentar en publicaciones de otros
  - Editar su perfil
  - Visualizar su propio contenido de forma privada

- **Administrador (opcional):** Puede realizar tareas de moderación como:
  - Eliminar u ocultar publicaciones ajenas
  - Restringir temporalmente o bloquear usuarios
  - (Este rol aún no está completamente definido ni implementado, pero se considera para versiones futuras)

---

## 2. Acciones por tipo de usuario

| Acción                                      | Invitado | Usuario Registrado | Administrador |
|---------------------------------------------|----------|--------------------|---------------|
| Ver posts públicos                          | ✅       | ✅                 | ✅            |
| Ver comentarios                             | ✅       | ✅                 | ✅            |
| Ver perfiles de usuario                     | ✅       | ✅                 | ✅            |
| Comentar en publicaciones                   | ❌       | ✅                 | ✅            |
| Crear publicaciones                         | ❌       | ✅                 | ✅            |
| Editar/eliminar propias publicaciones       | ❌       | ✅                 | ✅            |
| Editar perfil                               | ❌       | ✅                 | ✅            |
| Eliminar publicaciones ajenas               | ❌       | ❌                 | ✅            |
| Restringir/bloquear usuarios                | ❌       | ❌                 | ✅            |
| Crear cuenta                                | ✅       | —                  | —             |

---

## 3. Historias de Usuario

- Como **lector/visitante** quiero poder entrar a un post para leerlo.
- Como **usuario registrado** quiero poder dejar un comentario a un post.
- Como **usuario registrado** quiero poder crear un post.
- Como **lector/visitante** quiero poder crearme una cuenta.
- Como **usuario registrado** quiero poder visualizar mi lista de post.
- Como **usuario registrado** quiero poder modificar mi post.
- Como **usuario registrado** quiero poder seguir a otros usuarios (fuera del MVP).

---

## 4. Alcance del MVP

Las funcionalidades consideradas esenciales para el **Minimum Viable Product (MVP)** son:

- Lectura de publicaciones (por cualquier visitante)
- Registro e inicio de sesión de usuarios (con verificación por correo)
- Creación y edición de publicaciones por usuarios autenticados
- Comentarios en publicaciones (por usuarios registrados)
- Visualización del propio contenido (lista de publicaciones del usuario)
- Edición de perfil de usuario

**Fuera del MVP pero planeado a futuro:**

- Sistema de seguimiento o amistad entre usuarios
- Módulo de administración y moderación de contenido
- Notificaciones entre usuarios
- Integración de markdown enriquecido con gráficos
- Soporte para videollamadas o chat grupal
- Edicion/Eliminación de comentarios del propietario de la cuenta
