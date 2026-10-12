# 16. Infraestructura como código con Terraform

Fecha: 2026-10-11
Estado: Aceptado

## Contexto

La infraestructura (proyectos, Cloud Run, permisos, secretos, alertas de
presupuesto, dominio) se repite en staging y producción. Configurarla a mano
en la consola es difícil de repetir, de auditar y de recuperar si algo se borra.

## Decisión

- La infraestructura se define con **Terraform** en la carpeta `infra/`.
- El **estado** de Terraform se guarda en un bucket de Cloud Storage con
  versionado, no en la computadora local.
- Cambios de infraestructura pasan por PR: `terraform plan` en CI y
  `terraform apply` tras revisar.
- Forma de aprender: crear cada recurso primero a mano en la consola,
  entenderlo, borrarlo y luego escribirlo en Terraform.

## Alternativas consideradas

- **Pulumi.** Igual idea pero en un lenguaje de programación; menos
  presente en vacantes.
- **Consola manual.** Rápido al inicio, pero no reproducible ni auditable.

## Consecuencias

**Positivas**
- Staging y producción son idénticos por diseño.
- La infraestructura queda versionada y documentada en el repo.
- Estándar del mercado.

**Negativas**
- Curva de aprendizaje (HCL, estado, módulos).
- El archivo de estado puede contener datos sensibles y hay que protegerlo.
- Cambios hechos a mano en la consola generan *drift* (diferencias con el código).

**Cuándo revisar esta decisión:** no se prevé cambio.
