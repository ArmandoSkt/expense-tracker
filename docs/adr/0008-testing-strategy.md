# 8. Estrategia de pruebas del backend

Fecha: 2026-10-11
Estado: Aceptado

## Contexto

Necesitamos confianza para cambiar el código sin romper nada. Las pruebas
contra una base de datos en memoria (H2) pueden pasar y aun así fallar en
producción, porque H2 no se comporta igual que PostgreSQL (tipos, funciones,
bloqueos). También queremos que la arquitectura (ADR-0002) se respete
automáticamente.

## Decisión

- **Pruebas unitarias** con JUnit 5, AssertJ y Mockito, sobre todo para el
  dominio de los módulos hexagonales, sin Spring ni base de datos.
- **Pruebas de integración** con **Testcontainers**, que levanta un PostgreSQL
  real en Docker durante la prueba.
- **Pruebas de arquitectura** con Spring Modulith (y ArchUnit si hace falta),
  por ejemplo: el paquete `domain` no importa nada de Spring.
- Todas se ejecutan en CI y bloquean el PR si fallan.

## Alternativas consideradas

- **H2 en memoria.** Más rápido, pero da falsos positivos por diferencias con
  PostgreSQL.

## Consecuencias

**Positivas**
- Las pruebas de integración reflejan el comportamiento real de producción.
- Las violaciones de arquitectura se detectan en CI.

**Negativas**
- Se necesita Docker en local y en CI.
- Las pruebas de integración son más lentas (segundos por contenedor); hay
  que reutilizar contenedores entre pruebas.

**Cuándo revisar esta decisión:** si el tiempo total de pruebas en CI se
vuelve un problema.
