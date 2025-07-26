# Diagrama Entidad-Relación (ERD)

Este diagrama representa las relaciones clave entre las entidades principales del sistema.

```mermaid
erDiagram
    User ||--o{ Post : has
    User ||--o{ Comment : writes
    Post ||--o{ Comment : receives
    Post }o--|| Category : belongs_to
    Post ||--o{ Tag : has
    Tag ||--o{ Post : tagged_in

    User {
        string id
        string name
        string username
        string email
        string password
        datetime creation_date
        boolean deleted
    }

    Post {
        string id
        string title
        string content
        datetime publishedAt
        boolean deleted
    }

    Comment {
        string id
        string content
        datetime createdAt
        boolean deleted
    }

    Category {
        string id
        string name
        string description
    }

    Tag {
        string id
        string name
    }
```

## Descripción general

- **User** crea **Post** y escribe **Comment**
- **Post** recibe **Comment**, pertenece a una **Category** y tiene múltiples **Tag**
- **Tag** puede estar en múltiples **Post**
- Se usa eliminación lógica (`deleted`) en `User`, `Post` y `Comment` para evitar pérdida permanente de datos.

Este diagrama refleja el modelo de datos del MVP, sujeto a ajustes si se agregan nuevas funcionalidades como favoritos, historial de actividad, etc.
