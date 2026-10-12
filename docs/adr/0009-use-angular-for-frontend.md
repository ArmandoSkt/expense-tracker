# 9. Usar Angular para el frontend

Fecha: 2026-10-11
Estado: Aceptado

## Contexto

La aplicación necesita una interfaz web. El objetivo profesional es un perfil
"fullstack Java", y en LatAm muchas vacantes de Java corporativo (bancos,
consultoras) piden Angular. Tengo experiencia previa con NestJS, que está
inspirado en Angular.

## Decisión

Usaremos **Angular** con TypeScript, siguiendo las prácticas actuales del
framework (componentes *standalone* y *signals*). El cliente HTTP se genera
desde el contrato OpenAPI (ADR-0003).

## Alternativas consideradas

- **React + Vite.** Ecosistema más grande y aparece en más vacantes en
  general, pero requiere elegir router, formularios y estado por separado.
- **Vue.** Sencillo, pero menos presente en vacantes Java corporativas.

## Consecuencias

**Positivas**
- Framework completo con una forma oficial de hacer las cosas (router,
  formularios, HTTP, inyección de dependencias).
- Su estructura de servicios e inyección se parece a Spring y a NestJS.
- Alineado con vacantes "Java + Angular".

**Negativas**
- Curva de aprendizaje mayor que React o Vue.
- Más código base (*boilerplate*) para pantallas simples.
- Cambios de versión frecuentes; hay que mantenerse al día.

**Cuándo revisar esta decisión:** si las vacantes objetivo cambian hacia React.
