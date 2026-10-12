# 24. Convención de idiomas

Fecha: 2026-10-11
Estado: Aceptado

## Contexto

El proyecto busca, además, practicar inglés técnico. La documentación de
decisiones se entiende mejor en español, pero el código mezclado en dos
idiomas (`getGastosByCategory()`) es difícil de leer y de buscar.

## Decisión

| Qué | Idioma |
|---|---|
| Contenido de ADR y documentación | Español |
| Nombres de archivos y carpetas | Inglés |
| Código: clases, métodos, variables, tablas, endpoints | Inglés |
| Comentarios en el código | Inglés |
| Mensajes de commit | Inglés (Conventional Commits) |
| Issues y PR | Inglés |
| Textos de la interfaz para el usuario | Español (con soporte de i18n) |

## Alternativas consideradas

- **Todo en español.** Más cómodo, pero no practica el idioma y choca con las
  convenciones del ecosistema.
- **Todo en inglés.** Máxima práctica, pero las decisiones serían más difíciles
  de razonar al inicio.

## Consecuencias

**Positivas**
- Código consistente y alineado con el ecosistema.
- Práctica continua de inglés técnico.

**Negativas**
- Dos idiomas en el repo; hay que respetar la frontera.

**Cuándo revisar esta decisión:** si se suman colaboradores que no hablen español.
