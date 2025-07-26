# ADR 002 – Uso de Docker y Docker Compose para desarrollo y despliegue

## Contexto

El proyecto se compone de múltiples partes: frontend en React, backend en Express, y una base de datos MySQL. Para facilitar su ejecución en distintos entornos, así como su despliegue en servidores como Oracle Cloud o DigitalOcean, se decidió usar Docker para contenerizar cada componente.

Además, se optó por Docker Compose para orquestar los servicios durante el desarrollo y las pruebas, permitiendo levantar fácilmente todos los servicios necesarios desde un único archivo `docker-compose.yml`.

## Decisión

Cada componente del sistema (frontend, backend, base de datos) será ejecutado dentro de un contenedor Docker. El backend y frontend tendrán sus respectivos `Dockerfile` y serán construidos como imágenes independientes.

Se utilizará `docker-compose` en entornos de desarrollo y pruebas para facilitar la coordinación entre servicios. En producción, se usará también para definir redes internas, persistencia de volúmenes y configuración de entorno.

## Consecuencias

- \+ Aislamos cada componente en su propio contenedor, lo que permite mayor portabilidad
- \+ Facilita la replicación de entornos en distintos equipos o servidores
- \+ Permite automatizar despliegues con herramientas como GitHub Actions
- \+ Define infraestructura como código
- \- Requiere aprendizaje y mantenimiento de archivos Docker y Compose
- \- Aumenta el tiempo de build en cada cambio si no se optimizan bien las capas

## Estado

Aceptado – 23 de junio de 2025

