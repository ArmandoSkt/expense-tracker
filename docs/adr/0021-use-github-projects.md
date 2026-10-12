# 21. Gestión del proyecto con GitHub Projects

Fecha: 2026-10-11
Estado: Aceptado

## Contexto

Necesitamos organizar el trabajo (historias, tareas, bugs) y su avance. El
repositorio es público y también sirve para mostrar cómo se trabaja.

## Decisión

- Usaremos **GitHub Issues** para cada tarea y **GitHub Projects** como tablero.
- Cada PR referencia y cierra su issue (`Closes #12`).
- Etiquetas por tipo (`feat`, `bug`, `docs`, `chore`) y por módulo.
- Hitos (*milestones*) para cada fase del proyecto (MVP, primer despliegue, etc.).

## Alternativas consideradas

- **Jira.** Estándar en empresas, pero separado del código y excesivo para una persona.
- **Notion.** Flexible, pero no se vincula de forma natural con PR y commits.

## Consecuencias

**Positivas**
- Trabajo, código y PR en un solo lugar, con trazabilidad completa.
- El tablero público muestra el proceso de trabajo.

**Negativas**
- Menos funciones de reporte que Jira.
- No se practica Jira, que piden muchas vacantes.

**Cuándo revisar esta decisión:** no se prevé cambio.
