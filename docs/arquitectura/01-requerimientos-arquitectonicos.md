# Architectural Requirements – Blog Técnico Personal

## 1. Design Purpose

Este diseño arquitectónico tiene un propósito doble: por un lado, reorganizar y expandir un proyecto previo estático en Vue hacia una arquitectura completa con frontend, backend y persistencia de datos. Por otro lado, el proyecto es una plataforma personal que servirá como bitácora (técnica) para y como ejercicio de aprendizaje con tecnologías como React, Docker y CI/CD.

## 2. Primary Functionality

El sistema se basa en tres funcionalidades críticas:

- Gestión de usuarios (registro, inicio de sesión, autenticación)
- Creación y publicación de entradas de blog
- Sistema de comentarios en las entradas de blog

Estas tres funcionalidades son necesarias para que el proyecto cumpla su propósito. Esta pensado integrarle módulos adicionales, tales como un chat, soporte para markdown, diagramas y videollamadas, por ahora solo son complementarios y puramente orientados a practicar nuevas tecnologías.

## 3. Quality Attributes

Los atributos más relevantes son:

- **Seguridad**: Especialmente integridad y confidencialidad de contraseñas.
- **Escalabilidad**: Posibilidad de crecer funcionalmente con nuevos módulos (ejemplo: un modulo futuro de notificaciones), sin reescribir la arquitectura.
- **Mantenibilidad**: Deseable una arquitectura desacoplada, con módulos reutilizables, fácilmente sustituibles o escalables.

## 4. Constraints

- **Presupuesto**: Al ser un poryecto personal, se utilizará infraestructura gratuita (Oracle o servidor local), al igual que servicios económicos.
- **Tecnología base**: MySQL, Node/TypeScript, Docker.
- **Flexibilidad tecnológica**: Se permite el uso de MongoDB, Redis o incluso otros lenguajes si un módulo lo amerita (ya sea por mejorar eficiencia o practicar).

## 5. Architectural Concerns

- **Modularidad**: Interés por microservicios para módulos como notificaciones por email, que puedan reutilizarse en otros proyectos.
- **Evolutividad**: Posibilidad de añadir nuevos módulos (como videollamadas o reportes de bugs) sin acoplamiento rígido.
- **Patrón estructural**: Actualmente basado en MVC, pero se acepta evaluar y adoptar patrones como hexagonal, event-driven o incluso arquitecturas orientadas a flujos como Pipes & Filters.

