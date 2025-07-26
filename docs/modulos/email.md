# Diseño del Módulo – Email

## Objetivo

Diseñar el módulo `email` como componente reutilizable para el envío de correos electrónicos transaccionales en el sistema, como verificación de cuenta, restablecimiento de contraseña y notificaciones importantes. Está pensado para desacoplarse como microservicio en el futuro.

---

## Estructura del módulo
```
/modules/emails/
├── email.service.ts
├── templates/
│ ├── welcome.template.ts
│ └── resetPassword.template.ts
└── index.ts
```
---

## Flujos principales

### Enviar correo de verificación
1. Usuario se registra
2. Backend genera código de verificación y lo guarda temporalmente (cache)
3. `email.service` usa plantilla `welcome` y envía a correo proporcionado

### Enviar enlace para restablecer contraseña
1. Usuario solicita recuperación (`POST /api/auth/forgot-password`)
2. Se genera token temporal y se guarda
3. Se usa plantilla `resetPassword` y se envía

---

## Validaciones

- Correo debe ser válido
- El contenido debe tener versión en texto plano y HTML
- No se debe permitir spam desde una IP o usuario (limitar intentos)

---

## Dependencias

- `auth`: activa el flujo de verificación y recuperación
- `services/cache`: guarda códigos/verificaciones temporalmente
- `frontend`: recibe correos con links/códigos que abren rutas

---

## Posibles tareas técnicas u

- [ ] Abstraer `EmailService` con método `send(to, subject, html, text)`
- [ ] Soporte para plantillas dinámicas (nombre, código, link)
- [ ] Exportar funciones como `sendVerificationEmail(user)` o `sendResetEmail(user)`
- [ ] Logs en consola o archivo de cada envío

---

## Notas

- Puede desacoplarse como microservicio (`email-worker`) que escuche una cola (`queue`) y procese envíos en segundo plano
- Plantillas deben validarse para evitar XSS si se insertan datos del usuario
- Requiere archivo `.env` con configuración sensible: host, puerto, user, pass, from, etc.
