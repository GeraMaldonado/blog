# 🖥️ Vista Física del Sistema – Blog Técnico Personal

## Objetivo

Describir la distribución de los componentes del sistema en su entorno de ejecución, incluyendo contenedores, servidores, redes y comunicación entre servicios.

---

## 🧱 Infraestructura general

El sistema se despliega actualmente en un VPS gratuito de Oracle Cloud, con un entorno controlado mediante Docker. La infraestructura mínima incluye:

- **Servidor principal:** Oracle Cloud (Ubuntu VPS)
- **Orquestación:** `docker-compose` con múltiples servicios
- **Web server:** Nginx como proxy reverso
- **Base de datos:** MySQL, montada en volumen persistente

---

## 📦 Contenedores Docker

### 1. `frontend`

- Construido desde React + Vite
- Compilado y servido como archivos estáticos (por Nginx)

### 2. `backend`

- Aplicación Node.js con Express + TypeScript
- Expone API REST y sockets WebSocket (futuro)
- Conectado a la base de datos MySQL

### 3. `mysql`

- Contenedor oficial de MySQL
- Almacenamiento persistente en volumen `mysql_data`
- Expuesto solo internamente

> En el futuro, se contempla agregar servicios independientes como `email-service`, `notifications`, `scheduler`, etc., cada uno en su propio contenedor.

---

## 🌐 Redes y comunicación

- Todos los contenedores están conectados por red interna definida por Docker Compose
- `nginx` expone el puerto 80/443 y enruta:
  - `/api/` → `backend`
  - `/` → archivos estáticos del `frontend`

---

## 🔐 Seguridad

- Comunicación cifrada (plan futuro) con certificados SSL via Let’s Encrypt
- Acceso a MySQL restringido a la red interna
- Tokens JWT usados entre frontend y backend (por cookies)

---

## 🛠️ Automatización y CI/CD

- Se usa GitHub Actions para:
  - Lint y tests
  - Build de imágenes Docker
  - Deploy por SSH al VPS
- Las imágenes se construyen como multistage (`Dockerfile` optimizado)
- Nginx sirve como capa de proxy y caché de contenido estático

---

## Diagrama conceptual (texto)

```
[Internet]
    │
    ▼
[Nginx - Oracle VPS]
 ├── /api → [Backend Container]
 └── /     → [Frontend (static build)]

[Backend Container]
 ├── Express API
 └── Prisma → [MySQL Container]

[Frontend Container]
 └── React build (servido por Nginx)

[MySQL Container]
 └── Volumen persistente (mysql_data)
```

---

## Notas

Esta vista muestra un sistema desplegado de forma sencilla pero extensible, con separación clara de responsabilidades. La arquitectura facilita escalar con más contenedores o migrar servicios específicos a servidores o dominios distintos si el proyecto crece.

