# 25. Convención de idiomas (actualización: README en inglés)

Fecha: 2026-10-11
Estado: Aceptado
Reemplaza a: ADR-0024

## Contexto

El ADR-0024 estableció que toda la documentación se escribe en español. El
README principal, sin embargo, es la portada del repositorio y del
portafolio: es lo primero que leen reclutadores y otras personas, y muchas
de ellas no hablan español. Además, escribirlo en inglés es práctica directa
del idioma, uno de los objetivos del proyecto.

## Decisión

Se mantiene todo el ADR-0024, con un cambio: **el README principal se escribe
en inglés**.

| Qué | Idioma |
|---|---|
| README principal | **Inglés** (cambio) |
| Contenido de ADR y demás documentación | Español |
| Nombres de archivos y carpetas | Inglés |
| Código: clases, métodos, variables, tablas, endpoints | Inglés |
| Comentarios en el código | Inglés |
| Mensajes de commit | Inglés (Conventional Commits) |
| Issues y PR | Inglés |
| Textos de la interfaz para el usuario | Español (con soporte de i18n) |

## Alternativas consideradas

- **README en español.** Respeta el ADR-0024 sin cambios, pero limita a
  quién le sirve la portada del repositorio.
- **README bilingüe** (`README.md` en inglés y `README.es.md` en español).
  Llega a ambos públicos, pero hay que mantener dos versiones sincronizadas.

## Consecuencias

**Positivas**
- La portada del portafolio la entiende cualquier reclutador.
- Práctica de redacción técnica en inglés.

**Negativas**
- El README y los ADR que enlaza están en idiomas distintos.
- Una regla más que recordar en la convención.

**Cuándo revisar esta decisión:** si se suman colaboradores que no hablen
español (considerar ADR en inglés).
