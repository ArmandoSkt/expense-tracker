# 13. PostgreSQL gestionado en plan gratuito, migrar a Cloud SQL después

Fecha: 2026-10-11
Estado: Aceptado

## Contexto

Los datos son relacionales (usuarios, cuentas, categorías, transacciones,
presupuestos, apartados) y los reportes son agregaciones, así que usaremos
**PostgreSQL**. Cloud SQL no tiene plan gratuito y su instancia más pequeña
cuesta del orden de 10 USD al mes por entorno. Queremos empezar gastando
casi cero.

## Decisión

- Al inicio usaremos **PostgreSQL gestionado en plan gratuito** (Neon como
  opción preferida; Supabase como alternativa), en una región de la costa
  este de EE. UU. (ver ADR-0022).
- Habrá **una base de datos por entorno** (staging y producción); nunca se comparten.
- Conexión siempre con TLS; credenciales en Secret Manager.
- Migrar a **Cloud SQL** será un hito posterior, documentado en un ADR nuevo.

## Alternativas consideradas

- **Cloud SQL desde el inicio.** Todo dentro de GCP (red privada, IAM,
  respaldos), pero con costo fijo mensual que consume el presupuesto.
- **MongoDB / NoSQL.** Los datos son relacionales, el dinero necesita
  transacciones ACID y los reportes son agregaciones SQL.

## Consecuencias

**Positivas**
- Costo cercano a cero al inicio.
- La migración posterior es un buen ejercicio real (`pg_dump`/restore,
  tiempo fuera de servicio, validación).

**Negativas**
- La base de datos vive fuera de GCP: más latencia de red y conexión por
  internet público.
- Límites del plan gratuito (almacenamiento, cómputo, suspensión por
  inactividad) que hay que revisar.
- Un proveedor más que administrar.

**Cuándo revisar esta decisión:** al alcanzar los límites del plan gratuito
o cuando el presupuesto permita Cloud SQL.
