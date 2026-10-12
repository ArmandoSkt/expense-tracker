# 3. API REST con OpenAPI (code-first)

Fecha: 2026-10-11
Estado: Aceptado

## Contexto

El frontend en Angular necesita comunicarse con el backend. Hay un solo
cliente y los datos son poco anidados (gastos, categorías, presupuestos).
Si el contrato entre frontend y backend se mantiene a mano, tarde o temprano
se desincronizan: el backend cambia un campo y el frontend se entera en
producción.

## Decisión

- La API será **REST**, versionada en la ruta: `/api/v1/...`.
- El contrato se documenta con **OpenAPI**, generado desde el código del
  backend con **springdoc-openapi** (enfoque *code-first*).
- El frontend **genera su cliente TypeScript** a partir de ese contrato, en
  lugar de escribir las llamadas HTTP a mano.
- Los errores siguen un formato único (Problem Details, RFC 9457).

## Alternativas consideradas

- **GraphQL.** Útil con muchos clientes y datos muy anidados. Aquí agrega
  complejidad (caché, autorización por campo, problema N+1) sin beneficio.
- **Contract-first** (escribir primero el YAML de OpenAPI y generar las
  interfaces Java). Es común cuando varios equipos acuerdan la API antes de
  programar; con un solo desarrollador es más lento.

## Consecuencias

**Positivas**
- Si el backend cambia el contrato, el cliente generado deja de compilar y el
  error aparece en CI, no en producción.
- Documentación interactiva (Swagger UI) gratis en local y staging.
- REST es lo que más aparece en vacantes Java.

**Negativas**
- El contrato depende de anotaciones en el código; hay que cuidar que sean
  correctas y completas.
- Hay un paso extra en el build del frontend: regenerar el cliente.
- Swagger UI no debe exponerse en producción.

**Cuándo revisar esta decisión:** si aparecen otros clientes con necesidades
de datos muy distintas (por ejemplo, una app móvil nativa).
