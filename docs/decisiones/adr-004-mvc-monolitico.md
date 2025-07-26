# ADR 004 – Uso de arquitectura MVC modular en backend monolítico

## Contexto

El backend del sistema está desarrollado en Node.js con Express, utilizando una arquitectura tipo MVC (Modelo–Vista–Controlador). Esta estructura permite organizar el código en carpetas separadas por responsabilidad (`models`, `controllers`, `routes`, etc.), manteniendo una separación lógica entre datos, lógica de negocio y puntos de entrada HTTP.

Se eligió esta arquitectura para mantener claridad, facilitar el desarrollo incremental y permitir que cada recurso (usuarios, posts, comentarios) tenga su propio módulo independiente dentro del monolito.

## Decisión

Se mantendrá la arquitectura MVC modular dentro de un único servicio backend (monolito), estructurado por recurso y con routers independientes. Esta decisión se alinea con los objetivos actuales del proyecto: claridad, crecimiento controlado y facilidad de desarrollo.

Se utilizará Docker para contenerizar el backend y facilitar su despliegue, aceptando que la adición de nuevos módulos implica la reconstrucción de la imagen y el reinicio del servicio. Este comportamiento es aceptable dado que el sistema no está orientado a alta disponibilidad ni tráfico masivo.

## Consecuencias

- \+ Organización clara por responsabilidad y recurso (controladores, modelos, rutas)
- \+ Facilidad para extender nuevas funciones (crear carpetas como `comentarios/` y conectarlas al router)
- \+ Estructura sencilla de entender, ideal para proyectos personales o educativos
- \- Cada vez que se agrega una funcionalidad se debe reconstruir la imagen Docker y reiniciar el contenedor
- \- No está optimizado para escalar por módulo ni desplegar funcionalidades sin reinicio total
- \- Si el proyecto crece significativamente, se requerirá una reestructuración hacia una arquitectura más desacoplada (microservicios, hexagonal, etc.)

## Estado

Aceptado – 23 de junio de 2025

