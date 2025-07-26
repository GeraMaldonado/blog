# Diseño del Módulo – Categories

## Objetivo

Diseñar el módulo `categories` para organizar los posts en grandes bloques temáticos. A diferencia de `tags`, cada post debe pertenecer a una sola categoría, lo que permite estructurar el contenido de forma jerárquica o por tipo de tecnología/contenido.

---

## Estructura del módulo
```
/modules/categories/
├── categories.controller.ts
├── categories.router.ts
├── categories.model.ts
├── categories.validations.ts
├── dto/
│ └── categories.dto.ts
├── interfaces/
│ ├── ICategoriesModel.ts
│ └── ICategory.ts
└── index.ts
```

---

## Flujos principales

### Crear categoría (usuario)
1. Usuaeio autenticado accede a `POST /api/categories`
2. Se validan los datos (nombre único, descripción opcional)
3. Se guarda en base de datos
4. Se devuelve la nueva categoría

### Obtener todas las categorías
1. Cualquier usuario accede a `GET /api/categories`
2. Backend responde con lista ordenada alfabéticamente o por uso

### Asignar categoría a un post
1. Al crear/editar post se envía `categoryId`
2. Se valida que la categoría exista
3. Se asocia el `post` a esa `category`

---

## Validaciones

- Nombre: obligatorio, único, 3–30 caracteres
- Descripción: opcional, máximo 200 caracteres
- Solo una categoría por post 


---

## Dependencias

- `posts`: cada post debe tener un `categoryId` válido
- `frontend`: selector de categorías en formularios de post

---

## Posibles tareas técnicas 
- [ ] Endpoints:
  - `GET /api/categories` – listar
  - `GET /api/categories/:id` – detalle
  - `POST /api/categories` – crear (usuario)
  - `PUT /api/categories/:id` – editar (usuario)
  - `DELETE /api/categories/:id` – eliminar lógica (usuario)
- [ ] Tests para operaciones CRUD

---

## Notas

- Ideal para representar tecnologías (`Frontend`, `Backend`, `DevOps`) o propósitos (`Tutorial`, `Opinión`, `Proyecto`)
- Futuro: permitir jerarquías (categorías con subcategorías)
