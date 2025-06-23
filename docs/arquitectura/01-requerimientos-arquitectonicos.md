# 📐 Architectural Requirements – Blog Técnico Personal

## 1. Design Purpose

Este diseño arquitectónico tiene un propósito doble: por un lado, reorganizar y expandir un proyecto previo estático en Vue hacia una arquitectura completa con frontend, backend y persistencia de datos. Por otro lado, el proyecto es una plataforma personal que servirá como bitácora (técnica) para el autor/usuario y como ejercicio de aprendizaje con tecnologías como React, Docker y CI/CD.

## 2. Primary Functionality

El sistema se basa en tres funcionalidades críticas:

- Gestión de usuarios (registro, inicio de sesión, autenticación)
- Creación y publicación de entradas de blog
- Sistema de comentarios en entradas

Estas funcionalidades son necesarias para que el blog cumpla su propósito. Módulos adicionales como chat, markdown con soporte para diagramas o videollamadas son complementarios, orientados a práctica tecnológica.

## 3. Quality Attributes

Los atributos más relevantes son:

- **Seguridad**: Especialmente integridad y confidencialidad de contraseñas
- **Escalabilidad**: Posibilidad de crecer funcionalmente con módulos como notificaciones, sin reescribir la arquitectura
- **Mantenibilidad**: Deseable una arquitectura desacoplada, con módulos reutilizables, fácilmente sustituibles o escalables

## 4. Constraints

- **Presupuesto**: Se utilizará infraestructura gratuita (Oracle) o servicios económicos
- **Tecnología base**: MySQL, Node/TypeScript, Docker
- **Flexibilidad tecnológica**: Se permite el uso de MongoDB, Redis o incluso otros lenguajes si un módulo lo amerita

## 5. Architectural Concerns

- **Modularidad**: Interés por microservicios para módulos como notificaciones, que puedan reutilizarse en otros proyectos
- **Evolutividad**: Posibilidad de añadir nuevos módulos (como videollamadas o reportes de bugs) sin acoplamiento rígido
- **Patrón estructural**: Actualmente basado en MVC, pero se acepta evaluar y adoptar patrones como hexagonal, event-driven o incluso arquitecturas orientadas a flujos como Pipes & Filters

