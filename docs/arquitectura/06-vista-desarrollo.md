# Vista de Desarrollo – Blog Técnico Personal

## Objetivo

Describir la organización interna del código fuente del backend y frontend del sistema, con énfasis en la modularidad, capas lógicas y dependencias internas. Esta vista permite al desarrollador entender la estructura del sistema, facilitar su mantenimiento y permitir su evolución.

---

## Estructura actual del backend

El backend sigue una arquitectura **modular MVC**, con división por entidad (auth, posts, comments, etc.). Cada módulo incluye:

- `controller` → recibe la petición y delega
- `router` → define las rutas
- `service` → contiene la lógica de negocio
- `model.ts` → Prisma ORM
- `validations.ts` → validaciones con Zod/Yup/etc.
- `dtos/` → definiciones de objetos de transferencia
- `interfaces/` → tipos TS específicos

Adicionalmente:

- `emails/` → servicio de correo y plantillas (remplazar a futuro por modulo email aparte)
- `errors/` → manejadores y errores personalizados
- `services/` → servicios compartidos como cache o verificaciones
- `utils/` → utilidades generales
- `router/router.ts` → punto de entrada de rutas
- `index.ts` → servidor HTTP
- `database/` → conexión a base de datos por ORM

### Estructura deseada (reorganizable)

La recomienda es migrar hacia esta estructura:

```
/src
├── config/                # Variables, constantes, secretos
├── core/                  # Middlewares, errores, utilidades
├── modules/               # Cada funcionalidad del sistema
│   ├── auth/
│   ├── users/
│   ├── posts/
│   ├── comments/
│   └── notifications/     # Futura separación como microservicio
├── router/                # Punto central de rutas
└── index.ts               # Entry point
```

Esta uestructura facilita:

- Escalar con microservicios
- Reutilizar módulos en otros proyectos
- Separar dependencias con `index.ts` por módulo

---

## Frontend (proyectado)

El frontend se encuentra en desarrollo, pero se está alineando a una arquitectura React modular por componente, con carpetas para:

- `components/` → subcarpetas por dominio (`auth`, `posts`, `layout`, etc.)
- `pages/` → vistas de React Router
- `services/` → llamadas a la API REST
- `contexts/` → manejo de estado con React Context API
- `types/` → definiciones globales
- `hooks/` → hooks personalizados
- `utils/` → formateadores y helpers
- `routes/` → rutas centralizadas

Esto permite:

- Agrupación lógica por funcionalidades
- Separación clara de responsabilidades
- Soporte para futuras expansiones (chat, markdown enriquecido, etc.)

---

## Dependencias entre módulos

- `auth` depende de `users` para validar identidad
- `comments` y `posts` se relacionan entre sí por ID
- `emails` se usa desde `auth` y `notifications`
- `notifications` futura dependerá de `comments` y `posts`
- `router` importa todos los `router.ts` de módulos
- `middlewares` compartidos se usan en `router`

---

## Consideraciones futuras

- `notifications` y `emails` podrían extraerse como microservicios con Docker
- Si se adopta CQRS o eventos, se puede separar lectura/escritura
- La modularidad actual permite refactorizar a hexagonal sin grandes cambios

---

## Estado actual

- Backend ya funcional con MVC modular
- Frontend en transición hacia estructura recomendada
- Se documenta para facilitar mantenibilidad y escalabilidad
