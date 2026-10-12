# 22. Región de despliegue en la costa este de EE. UU.

Fecha: 2026-10-11
Estado: Aceptado

## Contexto

La base de datos gratuita (ADR-0013) corre sobre regiones de AWS, mientras
que el backend corre en GCP. Cada petición puede hacer varias consultas, y
cada consulta viaja entre los dos proveedores. Para la experiencia del
usuario pesa más la distancia backend–base de datos (varias idas y vueltas
por petición) que la distancia usuario–backend (una sola). Los usuarios
están en México.

## Decisión

- Backend en Cloud Run en **`us-east4`** (Virginia del Norte).
- Base de datos en **`us-east-1`** (Virginia del Norte, AWS).
- Medir la latencia real entre ambos al desplegar.

## Alternativas consideradas

- **Cloud Run en `northamerica-south1`** (Querétaro, México). Más cerca de
  los usuarios, pero lejos de la base de datos; cada consulta pagaría esa distancia.
- **`us-central1`.** Región principal de GCP, pero más lejos de la base de datos.

## Consecuencias

**Positivas**
- Latencia baja entre backend y base de datos.
- Latencia aceptable desde México.

**Negativas**
- Los datos residen fuera de México; debe indicarse en el aviso de privacidad.
- Si se migra a Cloud SQL, la región debe replantearse.

**Cuándo revisar esta decisión:** al migrar a Cloud SQL (ADR-0013) o si
aparecen requisitos de residencia de datos en México.
