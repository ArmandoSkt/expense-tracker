# 18. Trunk-based development y Conventional Commits

Fecha: 2026-10-11
Estado: Aceptado

## Contexto

Necesitamos un flujo de trabajo en Git que permita desplegar seguido y
mantener `main` siempre funcionando, con un historial fácil de leer.

## Decisión

- **Trunk-based development:** ramas cortas (horas o pocos días) que entran a
  `main` por PR. `main` siempre debe poder desplegarse.
- Nombres de rama: `feat/...`, `fix/...`, `docs/...`, `chore/...`.
- **Conventional Commits** en inglés: `feat: add expense registration`,
  `fix: rounding in monthly report`.
- `main` protegida: PR obligatorio, checks de CI en verde y commits firmados.
- Funciones incompletas se ocultan con *feature flags* en lugar de ramas largas.

## Alternativas consideradas

- **GitFlow** (`develop`, `release/*`, `hotfix/*`). Pensado para versiones
  planeadas; agrega ceremonia que no encaja con despliegue continuo.

## Consecuencias

**Positivas**
- Integración continua real y menos conflictos de merge.
- Changelog y versiones pueden generarse a partir de los commits.

**Negativas**
- Requiere disciplina para mantener los PR pequeños.
- Sin buenas pruebas en CI, `main` se puede romper.

**Cuándo revisar esta decisión:** si se necesitan mantener varias versiones
publicadas en paralelo.
