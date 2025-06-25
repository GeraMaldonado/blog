# ADR 003 – Verificación por correo electrónico antes del registro completo

## Contexto

Para registrar un nuevo usuario en el sistema, se implementó un paso previo de verificación por correo electrónico. El objetivo es prevenir registros masivos automáticos por bots, mejorar la integridad del sistema y asegurar que el correo proporcionado es válido y accesible por el usuario.

El flujo consiste en:
1. El usuario proporciona su nombre, correo y teléfono.
2. El backend genera un código de verificación y lo envía al correo electrónico.
3. El usuario debe ingresar ese código en el frontend para habilitar la creación efectiva de su cuenta.

Esta lógica también funciona como un filtro de seguridad básica y como paso inicial para futuras funciones como recuperación de contraseña o notificaciones.

## Decisión

El registro de usuarios solo será posible tras haber verificado el código enviado al correo electrónico del usuario. Mientras tanto, los datos del registro se almacenan temporalmente en cache (ej. NodeCache o Redis) y se validan antes de crear la entrada definitiva en la base de datos.

## Consecuencias

- ✅ Mejora la seguridad general del sistema al mitigar registros automáticos
- ✅ Valida correos electrónicos funcionales desde el inicio
- ✅ Permite construir sobre esta verificación futuras funciones como recuperación de cuenta o activación de features
- ⚠️ Requiere implementar lógica de expiración y almacenamiento temporal
- ⚠️ Agrega pasos adicionales al flujo de registro, lo cual puede afectar la conversión si no está bien diseñado

## Estado

Aceptado – 23 de junio de 2025

