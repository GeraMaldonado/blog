# Diseño del Módulo – Auth

## Objetivo

Definir la arquitectura y flujo del módulo `auth`, que gestiona el acceso al sistema mediante JWT, verificación de correo, recuperación de contraseña y protección de rutas. Este diseño asegura un control de sesiones seguro y modular.

---

## Estructura del módulo

```
/modules/auth/
├── auth.controller.ts
├── auth.router.ts
├── auth.service.ts
├── auth.model.ts
├── auth.validations.ts
├── protected.middleware.ts   
├── dtos/
│   └── auth.dto.ts
├── interfaces/
│   └── IUserAuth.ts
└── index.ts
```

---

## Flujo principal: Registro y login

### Registro
1. Usuario envía email, username y password
2. `auth.validations.ts` valida input
3. Se genera código y se envía correo con código temporal
4. Usuario introduce código -> se verifica y se crea cuenta
5. Se emite JWT y refresh token -> se guardan en cookies

### Login
1. Usuario envía credenciales
2. Se verifica usuario y contraseña
3. Se emite JWT y refresh token (ambos en cookies seguras)
4. Se responde con info básica del usuario

---

## Validaciones

- Email válido y único
- Password mínimo 8 caracteres, con mayúscula, número y símbolo
- Nombre de usuario sin espacios ni caracteres especiales
- Tokens deben ir en cookies HttpOnly + Secure (si HTTPS)

---

## Seguridad

- 2 tokens (acceso y refresh)
- JWT corto (15min) + refresh (7días)
- Sistema de rotación y revocación de tokens futuros
- Intentos fallidos limitados
- Dispositivos bloqueados tras múltiples intentos

---

## Dependencias

- `users`: para verificar existencia y recuperar info
- `emails`: envío de verificación y recuperación
- `cache`: guardado temporal de códigos (con TTL)
- `utils/encrypt`: para hasheo/verificación de contraseña

---

## Posibles tareas técnicas

- [ ] Endpoints:
  - `POST /auth/register`
  - `POST /auth/verify`
  - `POST /auth/login`
  - `POST /auth/logout`
  - `POST /auth/refresh-token`
  - `POST /auth/forgot-password`
  - `POST /auth/reset-password`
- [ ] Middleware `protected.middleware.ts`
- [ ] Validaciones con Zod/Yup
- [ ] Guardar sesiones y códigos con `NodeCache` (cambiar a `Redis` a futuro)
- [ ] Configurar rotación segura de tokens
- [ ] Añadir tests automatizados y documentación Swagger

---

## Notas

- El sistema actual está pensado para desacoplar el microservicio de correo
- El auth debe ser independiente a la base de datos (MySQL o Mongo)
- Las cookies manejan el acceso y el refresh de forma separada

