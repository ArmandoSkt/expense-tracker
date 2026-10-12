# 1. Usar un monorepo

Fecha: 2026-10-11
Estado: Aceptado

## Contexto

El proyecto tiene varias partes: un backend en Spring Boot, un frontend en
Angular, la infraestructura en GCP (Terraform) y la documentación.
Hay que decidir si todas viven en un solo repositorio o en repositorios separados.

Es un proyecto personal con una sola persona en el equipo. Muchos cambios
tocan varias partes a la vez; por ejemplo, agregar un campo a un gasto
requiere una migración, cambiar la API y actualizar el formulario.

## Decisión

Usaremos un monorepo con una carpeta por componente:

- `backend/` para la API en Spring Boot
- `frontend/` para la aplicación en Angular
- `infra/` para la infraestructura como código
- `docs/` para la documentación y los ADR

Cada componente se compila y despliega de forma independiente. Los pipelines
de GitHub Actions usan filtros por ruta para que un cambio en una carpeta
solo ejecute el pipeline de ese componente.

## Alternativas consideradas

**Un repositorio por componente.** Permite permisos y ciclos de versión
independientes, y es común cuando distintos equipos son dueños de cada parte.
Lo descartamos porque con una sola persona solo agrega coordinación: un cambio
que cruza backend y frontend necesitaría varios PR y cuidar el orden en que
se fusionan.

## Consecuencias

**Positivas**
- Un cambio que cruza varias partes se revisa y fusiona en un solo PR.
- El frontend genera su cliente desde el contrato OpenAPI del backend sin
  publicar paquetes entre repositorios.
- Issues, tablero, ADR y configuración de seguridad viven en un solo lugar.

**Negativas**
- Los pipelines necesitan filtros por ruta; si se configuran mal, se despliega
  de más o de menos.
- No es posible dar permisos solo a una parte del proyecto.
- El repositorio acumula el historial de todos los componentes.

**Cuándo revisar esta decisión:** si se suman equipos que necesiten
permisos o ciclos de despliegue separados.