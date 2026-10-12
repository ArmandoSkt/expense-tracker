# 2. Monolito modular con Spring Modulith y hexagonal selectiva

Fecha: 2026-10-11
Estado: Aceptado

## Contexto

El backend tiene áreas con complejidad muy distinta. Algunas son CRUD simple
(categorías, cuentas de origen como "Efectivo" o "Tarjeta"), y otras tienen
reglas de negocio reales: presupuestos con límites y porcentajes, apartados
cuyo saldo no puede quedar negativo y reportes con cálculos.

El equipo es de una persona y el tráfico esperado es bajo. Aun así, queremos
límites claros entre áreas para que el código no se enrede con el tiempo y
para poder extraer un servicio en el futuro si se justifica.

## Decisión

El backend será **una sola aplicación desplegable**, dividida en **módulos por
dominio** (un paquete de primer nivel por módulo: `expenses`, `categories`,
`accounts`, `budgets`, `savings`, `reports`).

- **Spring Modulith** verificará en las pruebas que ningún módulo use las clases
  internas de otro y que no haya dependencias circulares.
- Los módulos se comunican mediante su API pública o mediante **eventos**
  (por ejemplo, `ExpenseRegistered`).

La estructura interna de cada módulo sigue este criterio. Un módulo usa
**arquitectura hexagonal** (dominio sin Spring ni JPA, puertos y adaptadores)
si cumple al menos uno de estos puntos:

1. Tiene reglas de negocio que se pueden romper (saldos, límites, validaciones
   entre entidades).
2. Su lógica merece pruebas unitarias sin base de datos ni Spring.
3. Depende de algo externo que podría cambiar (proveedor de identidad,
   mensajería, correo).

Si no cumple ninguno, usa **capas simples**: `controller → service → repository`.

Regla para todos los módulos: la API expone DTOs, **nunca** entidades JPA.

Clasificación inicial:

| Módulo | Estilo |
|---|---|
| `categories` | Capas simples |
| `accounts` | Capas simples |
| `expenses` | Capas simples (puede evolucionar) |
| `budgets` | Hexagonal |
| `savings` | Hexagonal |
| `reports` | Hexagonal ligera |

## Alternativas consideradas

- **Microservicios.** Resuelven problemas de organización (muchos equipos,
  escalado independiente) que este proyecto no tiene. Traen transacciones
  distribuidas, fallos de red, más costo y más cold starts en Cloud Run.
- **Hexagonal en todos los módulos.** Da consistencia, pero agrega modelos,
  mappers e interfaces en módulos CRUD sin proteger ninguna regla.
- **Capas sin módulos.** Es lo más rápido al inicio, pero el acoplamiento crece
  sin control y después separar es muy costoso.
- **Vertical Slice Architecture.** Válida, pero poco común en el ecosistema
  Java y encaja peor con Spring Modulith.

## Consecuencias

**Positivas**
- Los límites entre módulos se verifican automáticamente en CI.
- La lógica de negocio importante se prueba aislada y rápido.
- Los eventos entre módulos facilitan extraer un servicio en el futuro.

**Negativas**
- Conviven dos estilos internos; quien lea el código necesita conocer el criterio.
- Cada módulo nuevo exige decidir su estilo.
- Migrar un módulo de capas simples a hexagonal tiene un costo de refactor.

**Cuándo revisar esta decisión:** si un módulo necesita escalar o desplegarse
de forma independiente, o si se suman equipos dueños de partes distintas.
