# 📆 Roadmap de Versiones – Blog Técnico Personal

## Objetivo

Establecer un plan de evolución funcional del sistema, dividiendo las funcionalidades en versiones incrementales. Cada versión agrupa historias de usuario o tareas técnicas y representa un hito alcanzable.

---

## 🟢 Versión MVP (v1.0)

### Funcionalidades principales
- Registro y autenticación de usuarios (JWT + verificación por correo)
- Crear, editar y eliminar posts (solo propios)
- Ver posts de otros usuarios
- Crear y ver comentarios en posts
- Panel de perfil básico (posts creados, datos básicos)
- Validaciones frontend y backend
- Docker + despliegue en VPS

### Tareas técnicas
- Configuración inicial de Prisma, rutas y middlewares
- Sistema de envío de correos (microservicio interno o acoplado)
- Testing básico con Supertest para rutas principales
- Documentación básica en Swagger

---

## 🟡 Versión 2 (v2.0)

### Nuevas funcionalidades
- Subida de imágenes de perfil y portada para posts
- Soporte para markdown enriquecido en posts
- Búsqueda de posts y usuarios
- Filtros por temas y etiquetas
- Visualización de posts más recientes, comentados y vistos
- Sistema de notificaciones básico (comentaron tu post)

### Tareas técnicas
- Servicio de archivos/imágenes (usando multer o cloud)
- Parser de markdown con bloques de código y Mermaid
- Algoritmo básico de ranking de posts (vistas, comentarios)
- Microservicio opcional de notificaciones

---

## 🟠 Versión 3 (v3.0)

### Expansiones sociales y de interacción
- Mensajes directos entre usuarios
- Seguimiento entre usuarios (followers)
- Panel de actividad personal (historial de acciones)
- Sistema de bloqueo y reportes de usuarios

### Tareas técnicas
- Servicio de mensajería (WebSocket o API REST privada)
- Modelo de relaciones usuario-usuario
- Lógica de visibilidad limitada por bloqueo
- Gestión de reportes para administrador

---

## 🔵 Versión 4 (v4.0+)

### Funcionalidades avanzadas
- Videollamadas entre usuarios
- Compartir archivos dentro del chat
- Panel de administración completo (eliminar contenido, usuarios)
- Acceso a métricas (número de usuarios, post más vistos)

### Tareas técnicas
- Integración WebRTC o SDK externo para videollamadas
- Sistema de archivos ligero por sesión de chat
- Rutas de administración protegidas y con validación
- Módulo de métricas (logs, estadísticas básicas)

---

## 📝 Notas finales

- Las versiones no tienen una fecha fija, pero están pensadas como hitos lógicos de complejidad creciente
- El sistema permite mantener una arquitectura modular con posibilidad de migrar partes a microservicios conforme se avanza
- La prioridad siempre es que cada versión funcione de forma autónoma y estable, antes de pasar a la siguiente

