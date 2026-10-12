# 4. Usar Maven como herramienta de build

Fecha: 2026-10-11
Estado: Aceptado

## Contexto

El backend en Java necesita una herramienta que descargue dependencias,
compile, ejecute pruebas y empaquete la aplicación. Las dos opciones
principales son Maven y Gradle. Uno de los objetivos del proyecto es
practicar lo que piden las vacantes Java corporativas.

## Decisión

Usaremos **Maven**, con el **Maven Wrapper** (`mvnw`) incluido en el repo para
que todos los entornos (local y CI) usen la misma versión.

## Alternativas consideradas

- **Gradle (Kotlin DSL).** Más rápido y flexible porque el build es código.
  Es común en Android y empresas tech, pero esa flexibilidad no aporta mucho
  en este proyecto, y Maven aparece más en vacantes corporativas.

## Consecuencias

**Positivas**
- Configuración declarativa y predecible; casi todos los proyectos Maven se
  ven igual.
- Muy documentado y estándar en bancos y corporativos.

**Negativas**
- El XML del `pom.xml` es verboso.
- Builds más lentos que Gradle en proyectos grandes (no es un problema a esta escala).
- Personalizar el build fuera de lo común es más difícil.

**Cuándo revisar esta decisión:** si los tiempos de build se vuelven un
problema o las vacantes objetivo piden Gradle.
