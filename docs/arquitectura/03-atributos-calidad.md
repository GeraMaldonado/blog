# 📊 Atributos de Calidad – Blog Técnico Personal

## Escenarios de Calidad

---

### 🔐 Escenario 1 – Seguridad ante intento de acceso no autorizado

- **Fuente de estímulo:** Usuario (o bot) con token manipulado o expirado
- **Estímulo:** Realiza un intento de acceso con un token inválido
- **Artefacto:** Sistema de autenticación (backend / middleware)
- **Ambiente:** Durante una sesión activa o tras la expiración del token
- **Respuesta:** El sistema invalida el token, limpia credenciales del localStorage y registra el intento fallido. Si hay 4 intentos seguidos, se limita el acceso por 15 minutos. Si los intentos continúan, el sistema escala el bloqueo hasta 1 semana y luego bloquea el dispositivo.
- **Medida de respuesta:** El sistema detecta y responde en menos de 1 segundo al intento no autorizado; la lógica de escalado se aplica correctamente en todos los casos.

**Narrativa:** Cuando un usuario intenta acceder con un token expirado o manipulado, el sistema debe invalidar la sesión, eliminar las credenciales guardadas localmente, notificar el error y aplicar una política de bloqueo progresivo si los intentos persisten.

---

### 💥 Escenario 2 – Seguridad ante ataques tipo inyección SQL o fuerza bruta

- **Fuente de estímulo:** Usuario o bot ejecutando múltiples intentos de ingreso con datos maliciosos
- **Estímulo:** Se reciben múltiples peticiones sospechosas en un periodo corto
- **Artefacto:** API de autenticación o entrada de datos
- **Ambiente:** Producción, tráfico activo
- **Respuesta:** El sistema bloquea temporalmente la IP o dispositivo al detectar más de 5 intentos anómalos en menos de 30 segundos; aplica espera progresiva antes de permitir nuevos intentos
- **Medida de respuesta:** La IP es bloqueada correctamente tras superar el umbral, y se registra en logs para revisión posterior

**Narrativa:** Si se detectan múltiples intentos sospechosos en poco tiempo (como en ataques de fuerza bruta o inyecciones), el sistema debe bloquear temporalmente la IP o dispositivo ofensivo y registrar el evento para posible revisión posterior.

---

### 🔧 Escenario 3 – Mantenibilidad y evolución del sistema

- **Fuente de estímulo:** Desarrollador
- **Estímulo:** Se solicita agregar un nuevo módulo (ej. notificaciones)
- **Artefacto:** Estructura modular del backend (routers y servicios)
- **Ambiente:** Durante desarrollo normal (sin refactorización global)
- **Respuesta:** El sistema permite agregar el nuevo módulo solo añadiendo su ruta y lógica al router correspondiente sin modificar módulos existentes
- **Medida de respuesta:** El nuevo módulo se puede integrar funcionalmente en menos de 2 semanas con impacto mínimo en el sistema existente

**Narrativa:** Cuando se desea agregar un nuevo módulo al backend, este debe poder integrarse con facilidad apuntando desde el router principal, sin necesidad de modificar otros módulos, y completarse funcionalmente en un plazo razonable.

---

### ⚙️ Escenario 4 – Rendimiento ante múltiples usuarios

- **Fuente de estímulo:** Usuarios concurrentes
- **Estímulo:** 50 usuarios intentan acceder, leer y comentar al mismo tiempo
- **Artefacto:** Backend (servidor Express) y contenedores Docker
- **Ambiente:** Producción, tráfico moderado
- **Respuesta:** El sistema escala usando múltiples contenedores de backend para distribuir la carga (horizontal scaling)
- **Medida de respuesta:** El sistema mantiene funcionalidad con un tiempo de respuesta aceptable (< 5s); no se producen caídas durante pruebas de carga

**Narrativa:** Si múltiples usuarios interactúan simultáneamente, el sistema debe poder escalar horizontalmente mediante contenedores Docker y mantener un rendimiento estable sin caídas visibles.

---

### ♻️ Escenario 5 – Disponibilidad y recuperación ante falla

- **Fuente de estímulo:** Falla del contenedor de backend
- **Estímulo:** El backend se apaga inesperadamente o requiere reinicio
- **Artefacto:** Contenedor Docker del backend
- **Ambiente:** En producción, durante operación normal
- **Respuesta:** El sistema se recupera con respaldo del contenedor o su reconstrucción automática; se mantienen respaldos semanales
- **Medida de respuesta:** El sistema puede estar fuera de línea hasta por 1 mes, pero debe tener respaldos activos al menos 1 o 2 veces por semana para permitir restauración rápida

**Narrativa:** En caso de que el contenedor backend falle, el sistema debe poder ser restaurado desde un backup reciente o reconstruido de forma automatizada, permitiendo continuidad aún si estuvo inactivo hasta un mes.

