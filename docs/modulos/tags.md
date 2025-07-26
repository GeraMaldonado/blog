# Diseño del Módulo – Tags

## Objetivo

Diseñar el módulo `tags` para permitir la clasificación temática de publicaciones mediante etiquetas reutilizables, facilitando la exploración de contenido, navegación por temas y filtrado avanzado.

---

## Estructura del módulo
```
/modules/tags/
├── tags.controller.ts
├── tags.router.ts
├── tags.model.ts
├── tags.validations.ts
├── interfaces/
│ └── ITag.ts
│ └── ITagModel.ts
└── index.ts
```
---

## Flujos principales

### Asociar etiquetas a post
1. Usuario crea o edita un post con una etiqueta
2. Se envían las etiquetas como array al backend (`POST /posts`)
3. Se validan y normalizan (ej. minúsculas, sin espacios duplicados)
4. Si no existen, se crean nuevas
5. Se vinculan al post vía relación m:m

### Obtener posts por etiqueta
1. Usuario hace clic en una etiqueta o busca por ella
2. Frontend hace `GET /tags/:name/posts`
3. Backend devuelve los posts asociados, ordenados por fecha

---

## Validaciones

- Nombre: obligatorio, 2 a 30 caracteres
- No duplicados
- Máximo 5 etiquetas por post
- Almacenamiento en formato normalizado (sin tildes, sin espacios repetidos)

---

## Dependencias

- `posts`: creación y edición incluye asignación de etiquetas

---

## Posibles tareas técnicas 

- [ ] Definir rutas:
  - `GET /api/tags` – listar todas
  - `GET /api/tags/popular`
  - `GET /api/tags/recent`
  - `GET /api/tags/:name/posts`
- [ ] Middleware opcional para normalizar etiquetas
- [ ] Tests de integración para creación y consulta

---

## Notas

- Se recomienda una estrategia de normalización y caching para búsquedas rápidas
- Puede ser útil almacenar contador de uso por etiqueta
- Ideal para usarse como filtro combinado con temas o categorías
