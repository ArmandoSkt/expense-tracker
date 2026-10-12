# 14. Alojar el frontend en Firebase Hosting

Fecha: 2026-10-11
Estado: Aceptado

## Contexto

El frontend en Angular, una vez compilado, son archivos estáticos (HTML, JS,
CSS). Necesitan servirse con HTTPS, dominio propio y buena velocidad, con
costo cercano a cero.

## Decisión

Usaremos **Firebase Hosting**: CDN global, certificado HTTPS automático,
dominio propio (`app.<dominio>`) y canales de vista previa por PR.

## Alternativas consideradas

- **Cloud Storage + Cloud CDN + Load Balancer.** Es como lo arma una empresa a
  mano, pero el balanceador tiene costo fijo mensual. Queda como tema de
  aprendizaje posterior.
- **Vercel.** Muy simple, pero fuera de GCP.

## Consecuencias

**Positivas**
- Gratis a esta escala y fácil de desplegar desde CI.
- Previews por PR para revisar cambios visuales antes de fusionar.

**Negativas**
- Menos control sobre caché y cabeceras que con un balanceador propio.
- El frontend y el backend quedan en dominios distintos (`app.` y `api.`),
  lo que requiere configurar CORS.

**Cuándo revisar esta decisión:** si se necesita un balanceador común para
frontend y backend o reglas avanzadas de seguridad (Cloud Armor).
