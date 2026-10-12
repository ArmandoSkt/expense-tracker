# 20. Observabilidad con Cloud Logging/Monitoring, OpenTelemetry y Sentry

Fecha: 2026-10-11
Estado: Aceptado

## Contexto

Cuando algo falle en producción necesitamos saber qué pasó, dónde y a quién
afectó, sin conectarnos a ningún servidor. También queremos alertas antes de
que los usuarios reporten el problema.

## Decisión

- **Logs** estructurados en JSON desde Spring Boot, enviados a Cloud Logging,
  con un identificador de traza por petición. Nunca se registran tokens ni
  datos financieros sensibles.
- **Métricas** con Spring Boot Actuator y Micrometer, visibles en Cloud Monitoring.
- **Trazas** con OpenTelemetry, enviadas a Cloud Trace.
- **Errores del frontend** con Sentry (plan gratuito).
- **Alertas** básicas: tasa de errores, latencia y presupuesto de GCP.

## Alternativas consideradas

- **Stack de Grafana** (Loki, Tempo, Prometheus). Muy buen aprendizaje, pero
  más infraestructura que mantener. Queda para una fase posterior; gracias a
  OpenTelemetry, cambiar de destino no requiere reinstrumentar el código.

## Consecuencias

**Positivas**
- Integrado con GCP y con poca operación.
- Instrumentación estándar y portable.

**Negativas**
- Los logs y métricas tienen cuotas gratuitas; hay que controlar el volumen.
- Las herramientas quedan repartidas entre GCP y Sentry.

**Cuándo revisar esta decisión:** al aprender el stack de Grafana o si los
costos de ingestión crecen.
