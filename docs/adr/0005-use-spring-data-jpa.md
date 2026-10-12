# 5. Usar Spring Data JPA para acceso a datos

Fecha: 2026-10-11
Estado: Aceptado

## Contexto

El backend guarda y consulta datos en PostgreSQL. La mayoría de las
operaciones son CRUD (crear, leer, actualizar, borrar), pero los reportes
("en qué gasto más por mes y categoría") requieren agregaciones (`SUM`,
`GROUP BY`) que un ORM no siempre expresa bien.

## Decisión

- Usaremos **Spring Data JPA** (con Hibernate) como forma principal de acceso a datos.
- Para reportes y consultas complejas usaremos **proyecciones** o
  **consultas nativas** en SQL.
- Por defecto las relaciones serán *lazy*, y revisaremos el SQL generado para
  evitar el problema N+1.

## Alternativas consideradas

- **jOOQ.** SQL con tipos seguros generados desde el esquema; excelente para
  consultas complejas, pero menos común en vacantes. Podría usarse solo en el
  módulo `reports` si las consultas crecen mucho.
- **JdbcClient / JdbcTemplate.** Control total del SQL, pero mucho código
  manual para el CRUD.

## Consecuencias

**Positivas**
- Muy poco código para operaciones CRUD.
- Es el estándar del mercado Java y tema frecuente en entrevistas.

**Negativas**
- Riesgos conocidos del ORM: N+1, *lazy loading* fuera de transacción,
  consultas ineficientes ocultas. Hay que aprender a detectarlos.
- Conviven dos formas de consultar (JPA y SQL nativo).

**Cuándo revisar esta decisión:** si las consultas de reportes se vuelven
difíciles de mantener con SQL nativo (considerar jOOQ en ese módulo).
