# Diseño del Módulo – Posts

## Objetivo

Diseñar la arquitectura interna del módulo `posts`, incluyendo estructura, flujo, validaciones y puntos de integración con otros módulos. Este diseño servirá como guía directa para su implementación.

---

## Estructura del módulo

```
/modules/posts/
├── posts.controller.ts
├── posts.router.ts 
├── posts.service.ts
├── posts.model.ts 
├── posts.validations.ts      
├── dto/
│   └── posts.dto.ts          
├── interfaces/
│   ├── IPost.ts              
│   └── IPostModel.ts         
└── index.ts                  
```

---

## Flujo principal: Crear un post

1. Usuario autenticado envía POST `/api/posts`
2. Middleware valida token JWT
3. `posts.validations.ts` valida cuerpo del request
4. `posts.service.ts` crea entrada en base de datos
5. `posts.controller.ts` responde con post creado
6. Se puede emitir evento para futuras notificaciones

---

## Validaciones

- Título (requerido, 5–100 caracteres)
- Contenido (requerido, mínimo 20 caracteres)
- Imagen de portada (opcional, tamaño máximo 2MB)
- Etiquetas (opcional, máximo 10 por post)
- Tema (obligatorio, debe coincidir con un tema registrado)

---

## Dependencias

- Requiere `auth` para validar usuario
- Se relaciona con:
  - `comments` por ID de post
  - `tags` para categorizar
  - `users` para mostrar autor del post
  - `notifications` (futuro): para avisos de interacciones

---

## Posibles tareas técnicas 

- [ ] Definir rutas REST:
  - `POST /api/posts`
  - `GET /api/posts`
  - `GET /api/posts/:id`
  - `PUT /api/posts/:id`
  - `DELETE /api/posts/:id`
- [ ] Validar y sanitizar entrada
- [ ] Añadir tests automatizados con Supertest
- [ ] Integrar Swagger (descripción de rutas)
- [ ] Relacionar con módulo `users` (autor)
- [ ] Emitir evento cuando se cree/modifique un post

---

## Notas

- Se proyecta que este módulo pueda escalar para aceptar markdown enriquecido
- El diseño contempla separación entre lógica de presentación y negocio
- Se recomienda que las respuestas usen DTOs para evitar exponer internamente el modelo completo

