# ADR 001 – Uso de Prisma como ORM

## Contexto

Durante el desarrollo del backend del blog técnico personal, se tomó la decisión de incorporar un ORM para facilitar la gestión de la base de datos (inicialmente MySQL). La motivación principal fue contar con una herramienta que permitiera:

- Migraciones controladas sin necesidad de archivos `.sql`
- Facilidad para cambiar el sistema gestor (por ejemplo, de MySQL a PostgreSQL)
- Seguimiento de cambios estructurales en la base de datos
- Tipado automático al trabajar con TypeScript

Aunque existen otras opciones como Sequelize o TypeORM, no se realizó una comparación formal. La elección se basó en la percepción de que Prisma ofrecía una experiencia más moderna y declarativa, especialmente para desarrolladores que ya usan TypeScript.

## Decisión

Se adoptó Prisma como ORM principal para el backend del sistema. Se utilizará junto con MySQL para desarrollo y producción, permitiendo la generación automática del cliente de base de datos y las migraciones.

## Consecuencias

- ✅ Simplificación del acceso a datos mediante un cliente autogenerado y tipado
- ✅ Posibilidad de aplicar migraciones controladas desde código
- ✅ Portabilidad entre motores SQL
- ⚠️ Añade una dependencia externa considerable al proyecto
- ⚠️ Posible falta de soporte o cambios en la comunidad a largo plazo
- ⚠️ Si Prisma se abandona o deja de mantenerse, se necesitará migrar el ORM o trabajar directamente con SQL

## Estado

Aceptado – 23 de junio de 2025

