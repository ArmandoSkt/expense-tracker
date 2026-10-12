# 6. Usar Flyway para migraciones de base de datos

Fecha: 2026-10-11
Estado: Aceptado

## Contexto

La estructura de la base de datos cambiará con el tiempo (tablas y columnas
nuevas). Hay tres entornos (local, staging y producción) y todos deben tener
exactamente la misma estructura. Hacer los cambios a mano es propenso a errores.

## Decisión

- Usaremos **Flyway**. Cada cambio será un archivo SQL numerado
  (`V1__create_expenses.sql`, `V2__add_currency.sql`) que se aplica al
  arrancar la aplicación.
- Hibernate **nunca** crea ni modifica tablas: `ddl-auto=validate` en todos
  los entornos desplegados.
- Una migración ya aplicada no se edita; los errores se corrigen con una
  migración nueva.

## Alternativas consideradas

- **Liquibase.** Más funciones (rollback, varios formatos, varios motores),
  pero más complejo de leer.
- **`ddl-auto=update`.** Rápido, pero no controlamos qué SQL se ejecuta y
  puede romper datos en producción.

## Consecuencias

**Positivas**
- Todos los entornos tienen la misma estructura.
- Cada cambio de esquema queda versionado en Git y se revisa en un PR.
- El SQL que se ejecuta es exactamente el que se lee.

**Negativas**
- Hay que escribir SQL a mano para cada cambio.
- No hay rollback automático en la versión gratuita: deshacer requiere
  otra migración.
- Cambios grandes en tablas con muchos datos requieren planear migraciones
  sin bloqueos.

**Cuándo revisar esta decisión:** si se necesita soportar varios motores de
base de datos.
