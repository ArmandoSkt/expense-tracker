# Registro de decisiones de arquitectura (ADR)

Cada archivo de esta carpeta documenta una decisión importante del proyecto:
el contexto, lo que se decidió, las alternativas y sus consecuencias.

## Reglas

- Un ADR por decisión, numerado con 4 dígitos. Los números no se reutilizan.
- Para crear uno nuevo, copia `template.md`.
- Un ADR aceptado **no se edita**: si la decisión cambia, se escribe uno nuevo
  que lo reemplaza y el anterior pasa a "Reemplazado por ADR-XXXX".
- Contenido en español; nombre de archivo en inglés (ver ADR-0024).

## Índice

| # | Decisión | Estado |
|---|---|---|
| [0001](0001-use-monorepo.md) | Usar un monorepo | Aceptado |
| [0002](0002-modular-monolith-with-spring-modulith.md) | Monolito modular con Spring Modulith y hexagonal selectiva | Aceptado |
| [0003](0003-rest-api-with-openapi-code-first.md) | API REST con OpenAPI (code-first) | Aceptado |
| [0004](0004-use-maven.md) | Usar Maven | Aceptado |
| [0005](0005-use-spring-data-jpa.md) | Usar Spring Data JPA | Aceptado |
| [0006](0006-use-flyway-for-migrations.md) | Usar Flyway para migraciones | Aceptado |
| [0007](0007-money-representation.md) | Representación del dinero | Aceptado |
| [0008](0008-testing-strategy.md) | Estrategia de pruebas del backend | Aceptado |
| [0009](0009-use-angular-for-frontend.md) | Usar Angular para el frontend | Aceptado |
| [0010](0010-pwa-after-first-deploy.md) | PWA después del primer despliegue | Aceptado |
| [0011](0011-use-firebase-auth.md) | Firebase Auth / Identity Platform | Aceptado |
| [0012](0012-use-cloud-run-for-backend.md) | Backend en Cloud Run | Aceptado |
| [0013](0013-managed-postgres-free-tier.md) | PostgreSQL gestionado gratuito, Cloud SQL después | Aceptado |
| [0014](0014-use-firebase-hosting-for-frontend.md) | Frontend en Firebase Hosting | Aceptado |
| [0015](0015-separate-environments-per-gcp-project.md) | Entornos en proyectos de GCP separados | Aceptado |
| [0016](0016-use-terraform.md) | Infraestructura como código con Terraform | Aceptado |
| [0017](0017-github-actions-with-workload-identity.md) | CI/CD con GitHub Actions y Workload Identity | Aceptado |
| [0018](0018-trunk-based-development.md) | Trunk-based y Conventional Commits | Aceptado |
| [0019](0019-code-quality-and-supply-chain.md) | Calidad de código y seguridad de dependencias | Aceptado |
| [0020](0020-observability.md) | Observabilidad | Aceptado |
| [0021](0021-use-github-projects.md) | Gestión con GitHub Projects | Aceptado |
| [0022](0022-region-us-east.md) | Región en la costa este de EE. UU. | Aceptado |
| [0023](0023-domain-and-dns-on-cloudflare.md) | Dominio y DNS en Cloudflare | Aceptado |
| [0024](0024-language-conventions.md) | Convención de idiomas | Aceptado |
