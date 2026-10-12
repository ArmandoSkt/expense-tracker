# 19. Calidad de código y seguridad de dependencias

Fecha: 2026-10-11
Estado: Aceptado

## Contexto

El repositorio es público y será parte de un portafolio. Queremos detectar
errores, vulnerabilidades y deuda técnica de forma automática, y mantener las
dependencias actualizadas sin hacerlo a mano.

## Decisión

- **Formato automático:** Spotless en el backend; Prettier y ESLint en el frontend.
- **Análisis estático y cobertura:** SonarQube Cloud (antes SonarCloud).
- **Seguridad del código:** CodeQL para Java y TypeScript.
- **Dependencias:** Dependabot (alertas y actualizaciones de seguridad) y
  actualizaciones de versión configuradas por archivo.
- **Secretos:** Secret scanning y Push protection activos (ya habilitados).
- Los checks se ejecutan en cada PR y bloquean el merge si fallan.

## Alternativas consideradas

- **Solo formateador y linter.** Más simple, pero no detecta vulnerabilidades
  ni dependencias desactualizadas.

## Consecuencias

**Positivas**
- Problemas detectados antes de llegar a `main`.
- Herramientas gratuitas para repos públicos.

**Negativas**
- Más tiempo de CI y posibles falsos positivos que hay que revisar.
- Muchos PR automáticos de dependencias si no se agrupan.

**Cuándo revisar esta decisión:** si el ruido de alertas supera su utilidad.
