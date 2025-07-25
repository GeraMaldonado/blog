# Escenarios de Calidad – Blog Técnico Personal

## Objetivo

Especificar escenarios de calidad concretos para validar los atributos arquitectónicos definidos previamente: seguridad, mantenibilidad, escalabilidad y disponibilidad. Estos escenarios permiten evaluar el diseño y anticipar mecanismos de mitigación o mejora.

---

## Seguridad

### Escenario 1: Acceso con token vencido o manipulado
- **Fuente de estímulo**: Usuario autenticado con token JWT
- **Estímulo**: El token enviado en cookies ha expirado o fue alterado
- **Artefacto**: Middleware de autenticación y validación JWT
- **Ambiente**: Tiempo de ejecución (al hacer peticiones al backend)
- **Respuesta**:
  - Detectar token inválido
  - Invalidar sesión en frontend (borrar localStorage y cookies)
  - Mostrar mensaje de error y bloquear reintentos
- **Medida**: Se bloquea acceso tras 4 intentos inválidos, con tiempo de baneo progresivo (15 min, 1 hora, 1 semana)

### Escenario 2: Intento masivo de inyección SQL
- **Fuente de estímulo**: Atacante automatizado
- **Estímulo**: Múltiples peticiones maliciosas en poco tiempo
- **Artefacto**: Backend y motor de base de datos
- **Ambiente**: Tiempo de ejecución bajo carga maliciosa
- **Respuesta**:
  - Detección por patrones
  - Bloqueo temporal de IP o dispositivo
- **Medida**: Rechazo automático tras 10 intentos en <30s

---

## Mantenibilidad

### Escenario 3: Agregar nuevo módulo (por ejemplo, reportes de bugs)
- **Fuente de estímulo**: Desarrollador
- **Estímulo**: Solicita nueva funcionalidad
- **Artefacto**: Backend (estructura modular)
- **Ambiente**: Entorno de desarrollo
- **Respuesta**:
  - Crear carpeta con controladores, rutas, modelos y validaciones
  - Conectarlo en `router.ts` principal
  - Sin modificar funcionalidades existentes
- **Medida**: Tiempo estimado de integración < 3 días, sin afectar otros módulos

---

## Escalabilidad

### Escenario 4: Aumento de usuarios activos simultáneos
- **Fuente de estímulo**: Usuarios concurrentes
- **Estímulo**: 100 usuarios se conectan en menos de 1 minuto
- **Artefacto**: Contenedor de backend
- **Ambiente**: Producción en VPS
- **Respuesta**:
  - Backend responde a peticiones
  - Sistema puede levantar otro contenedor si se requiere
- **Medida**: Respuesta promedio < 800 ms en escenarios simulados

---

## Disponibilidad y Respaldo

### Escenario 5: Falla completa del VPS
- **Fuente de estímulo**: VPS deja de responder
- **Estímulo**: Corte eléctrico o caída del proveedor
- **Artefacto**: Docker + archivos persistentes
- **Ambiente**: Tiempo de inactividad
- **Respuesta**:
  - Respaldos semanales restauran el sistema
  - Contenedores se pueden reconstruir rápidamente
- **Medida**: Recuperación completa del sistema en < 24 horas
