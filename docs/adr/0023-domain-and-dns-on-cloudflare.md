# 23. Dominio y DNS en Cloudflare

Fecha: 2026-10-11
Estado: Aceptado

## Contexto

La app necesita un dominio propio para compartirla. El backend (Cloud Run) y
el frontend (Firebase Hosting) deben tener subdominios con HTTPS. Google
Domains ya no existe.

## Decisión

- Comprar el dominio en **Cloudflare Registrar** (precio de costo).
- Administrar el **DNS en Cloudflare** (gratis).
- Estructura:
  - `<dominio>`: página de presentación (fase posterior).
  - `app.<dominio>`: frontend en Firebase Hosting.
  - `api.<dominio>`: backend en Cloud Run.
- Certificados HTTPS emitidos por Firebase Hosting y Cloud Run.
- Registros DNS gestionados con Terraform (proveedor de Cloudflare).

## Alternativas consideradas

- **Otro registrador + Cloud DNS de GCP.** Más aprendizaje de GCP, pero Cloud
  DNS tiene costo mensual por zona.

## Consecuencias

**Positivas**
- Costo mínimo y DNS rápido con protección básica.

**Negativas**
- Un proveedor más fuera de GCP.
- Si se activa el proxy de Cloudflare, puede interferir con la emisión de
  certificados de Google; los registros de `app` y `api` empiezan en modo
  "solo DNS".

**Cuándo revisar esta decisión:** si se adopta un balanceador de GCP con
Cloud DNS.
