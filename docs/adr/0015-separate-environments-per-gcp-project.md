# 15. Entornos separados en proyectos de GCP distintos

Fecha: 2026-10-11
Estado: Aceptado

## Contexto

Necesitamos probar cambios antes de que lleguen a los usuarios. Si staging y
producción comparten recursos o permisos, un error en staging puede afectar
producción.

## Decisión

Habrá tres entornos:

| Entorno | Dónde | Datos |
|---|---|---|
| Local | Docker Compose en la computadora | Datos de prueba |
| Staging | Proyecto GCP `expense-tracker-stg` | Base de datos propia, datos de prueba |
| Producción | Proyecto GCP `expense-tracker-prod` | Base de datos propia, datos reales |

- Cada entorno tiene su propia base de datos, secretos y cuentas de servicio.
- Los datos reales nunca se copian a staging.
- Todo cambio pasa por staging antes de producción.

## Alternativas consideradas

- **Solo local + producción.** Más barato y simple, pero los errores se
  descubren directamente con usuarios.
- **Staging y producción en el mismo proyecto.** Menos aislamiento de permisos.

## Consecuencias

**Positivas**
- Aislamiento real: un permiso de staging no sirve en producción.
- Con Cloud Run escalando a cero, staging casi no cuesta.

**Negativas**
- Más configuración (dos proyectos, dos bases de datos, dos sets de secretos).
- Se mitiga con Terraform (ADR-0016): mismos archivos, distintas variables.

**Cuándo revisar esta decisión:** si se necesitan entornos efímeros por PR.
