# 17. CI/CD con GitHub Actions y Workload Identity Federation

Fecha: 2026-10-11
Estado: Aceptado

## Contexto

Cada cambio debe compilarse, probarse y desplegarse de forma automática y
repetible. El pipeline necesita permisos en GCP para desplegar. La forma
tradicional es guardar una llave JSON de cuenta de servicio como secreto en
GitHub, pero esa llave no expira y, si se filtra, da acceso permanente.

## Decisión

- Usaremos **GitHub Actions**, con un workflow por componente y **filtros por
  ruta** (`backend/**`, `frontend/**`, `infra/**`), como se acordó en ADR-0001.
- La autenticación con GCP será con **Workload Identity Federation**: GitHub
  obtiene un token temporal sin guardar ninguna llave.
- Flujo: PR → build y pruebas; merge a `main` → despliegue a staging;
  producción con aprobación manual.
- Cada entorno usa su propia cuenta de servicio con los permisos mínimos.

## Alternativas consideradas

- **Cloud Build.** Integrado con GCP, pero más atado a ese proveedor y menos
  común en vacantes.
- **Llaves JSON en secretos de GitHub.** Simple, pero inseguro.

## Consecuencias

**Positivas**
- Cero llaves de larga duración guardadas.
- El pipeline vive junto al código y se revisa en PR.

**Negativas**
- La configuración inicial de Workload Identity es más compleja.
- Hay que limitar qué repo y rama pueden asumir cada identidad.

**Cuándo revisar esta decisión:** si los minutos gratuitos de Actions no alcanzan.
