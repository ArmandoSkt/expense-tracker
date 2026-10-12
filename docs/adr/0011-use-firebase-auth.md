# 11. Usar Firebase Auth / Identity Platform como proveedor de identidad

Fecha: 2026-10-11
Estado: Aceptado

## Contexto

La app será pública y guardará datos financieros de otras personas. La
autenticación (registro, login, recuperación de contraseña, verificación de
correo, login social) es una de las partes más riesgosas de construir a mano.
Queremos aprender OAuth2/OIDC, que es lo que piden las vacantes.

## Decisión

- La identidad la maneja **Firebase Authentication / Google Identity Platform**.
- El frontend obtiene un **token JWT** al iniciar sesión.
- El backend actúa como **OAuth2 Resource Server** con Spring Security:
  valida la firma, emisor, audiencia y expiración del JWT en cada petición.
- Cada dato se filtra por el usuario del token; un usuario nunca puede leer
  datos de otro.

## Alternativas consideradas

- **Keycloak autohospedado.** Se aprende OIDC a fondo y aparece en vacantes,
  pero es otro servicio que asegurar, actualizar, respaldar y pagar siempre
  encendido. Se usará en local como ejercicio de aprendizaje.
- **Auth0 / Clerk.** Similar a Firebase, pero de terceros y fuera de GCP.
- **Autenticación propia.** Demasiado riesgo y trabajo para un proyecto
  público.

## Consecuencias

**Positivas**
- No guardamos contraseñas.
- Gratis a esta escala y nativo de GCP.
- Gracias a OIDC, cambiar de proveedor implica sobre todo cambiar la URL del emisor.

**Negativas**
- Dependemos de un proveedor externo (*vendor lock-in* parcial).
- Los usuarios viven en Firebase y no en nuestra base de datos; hay que
  sincronizar el identificador del usuario.
- Se aprende menos del lado del servidor de identidad.

**Cuándo revisar esta decisión:** si se necesitan funciones que Firebase no
ofrece (por ejemplo, roles complejos por organización).
