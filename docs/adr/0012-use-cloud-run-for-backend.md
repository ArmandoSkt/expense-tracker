# 12. Ejecutar el backend en Cloud Run

Fecha: 2026-10-11
Estado: Aceptado

## Contexto

El backend en Spring Boot necesita correr en GCP. El tráfico será bajo e
irregular (uso personal y de amigos), el presupuesto es de ~10 USD al mes y
no queremos administrar servidores.

## Decisión

- El backend se empaqueta como **imagen Docker**, se publica en **Artifact
  Registry** y se ejecuta en **Cloud Run**.
- Escala de 0 a pocas instancias (`min-instances=0` al inicio).
- Aceptamos el *cold start* de la JVM al principio y lo mediremos; las
  optimizaciones (CDS, GraalVM Native Image o `min-instances=1`) serán una
  tarea posterior basada en datos.

## Alternativas consideradas

- **GKE Autopilot (Kubernetes).** Muy demandado en vacantes, pero tiene costo
  base y complejidad excesiva para esta app. Se aprenderá aparte en local.
- **Compute Engine (VM).** Requiere instalar, actualizar y asegurar el
  servidor a mano.

## Consecuencias

**Positivas**
- Se paga casi solo por uso; con escala a cero el costo es muy bajo.
- HTTPS, escalado y despliegues por revisión incluidos.

**Negativas**
- Cold start: la primera petición tras un periodo sin uso puede tardar
  varios segundos.
- Límites de la plataforma (tiempo por petición, sin estado local entre
  instancias).

**Cuándo revisar esta decisión:** si el cold start afecta demasiado la
experiencia o la carga requiere procesos permanentes.
