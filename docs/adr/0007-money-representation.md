# 7. Representación del dinero

Fecha: 2026-10-11
Estado: Aceptado

## Contexto

La aplicación maneja montos de dinero. Los tipos de punto flotante (`double`,
`float`) no representan decimales con exactitud (`0.1 + 0.2 != 0.3`), y en
dinero esos errores se acumulan. Hoy solo se usará MXN, pero agregar la moneda
después a datos existentes sería costoso.

## Decisión

- En la base de datos: `NUMERIC(19,4)` para el monto y una columna
  `currency` (código ISO 4217, por ejemplo `MXN`).
- En Java: `BigDecimal`, envuelto en un **value object propio `Money`**:
  inmutable, con monto y moneda, que impide operar entre monedas distintas
  y centraliza el redondeo.
- Prohibido usar `double` o `float` para montos.

## Alternativas consideradas

- **Centavos como entero** (`BIGINT` / `long`). Correcto y usado por pasarelas
  de pago, pero menos legible y requiere convertir en cada frontera.
- **Librerías (Joda-Money, JSR 354 / Moneta).** Completas, pero agregan una
  dependencia y quitamos el ejercicio de diseñar un value object.

## Consecuencias

**Positivas**
- Cálculos exactos.
- Soporte de varias monedas sin migrar datos en el futuro.
- Las reglas de dinero viven en un solo lugar y se prueban aisladas.

**Negativas**
- `BigDecimal` es más verboso y hay que cuidar `equals` (compara escala) y el
  modo de redondeo.
- Hay que mapear `Money` entre dominio, JPA y DTOs.

**Cuándo revisar esta decisión:** si se agrega conversión entre monedas
(requiere tipos de cambio y fechas).
