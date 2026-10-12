# 10. Convertir la app en PWA después del primer despliegue

Fecha: 2026-10-11
Estado: Aceptado

## Contexto

Queremos registrar gastos rápido desde el teléfono. Una PWA (Progressive Web
App) se puede instalar en la pantalla de inicio y sentirse como app. Sin
embargo, una PWA **no puede crear widgets** nativos en iOS ni Android, y su
*service worker* (la pieza que cachea archivos) puede causar errores de caché
confusos mientras la app cambia mucho.

## Decisión

- Primero se construye y despliega la app web normal.
- Después del primer despliegue estable, se agrega soporte PWA
  (`@angular/pwa`: manifiesto, íconos y service worker).
- Para registrar gastos rápido desde el teléfono, en una fase posterior se
  evaluará un endpoint para Atajos de iOS / automatizaciones de Android antes
  de considerar un widget nativo.

## Alternativas consideradas

- **PWA desde el inicio.** Poco trabajo extra, pero bugs de caché durante el
  desarrollo temprano.
- **App o widget nativo.** Otro proyecto completo (Swift/Kotlin, cuenta de
  Apple Developer de pago).

## Consecuencias

**Positivas**
- El desarrollo inicial es más simple.
- La PWA se agrega cuando la app es estable.

**Negativas**
- Al inicio la app no es instalable ni funciona sin conexión.
- Habrá que definir una estrategia de actualización del service worker.

**Cuándo revisar esta decisión:** si se necesita un widget real en la
pantalla de inicio.
