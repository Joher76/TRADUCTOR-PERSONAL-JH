# TraductorPersonal_Android_0.4

Aplicación Android nativa para traducción bidireccional por turnos, con español como idioma principal.

## Funciones incluidas

- Identificación automática del idioma de un texto entrante con ML Kit Language Identification.
- Traducción texto entrante → español.
- Traducción español → idioma elegido.
- Dictado de voz para ambos turnos mediante Android `RecognizerIntent` / servicio de reconocimiento instalado.
- Lectura en voz alta mediante Android TextToSpeech.
- Descarga bajo demanda y uso local de modelos de traducción de ML Kit.
- Workflow de GitHub Actions para compilar y publicar el APK debug como artefacto.

## Requisitos

- Android Studio reciente (JDK 17).
- Android 6.0 (API 23) o superior.
- Para compilar: conexión a Internet para descargar dependencias.
- Para la primera traducción de cada par de idiomas: conexión a Internet para descargar los modelos de ML Kit.

## Compilar en Android Studio

1. Abre la carpeta raíz del proyecto.
2. Espera la sincronización de Gradle.
3. Ejecuta la configuración `app`.
4. Para generar APK: **Build → Build Bundle(s) / APK(s) → Build APK(s)**.

Desde una terminal con Gradle instalado:

```bash
gradle --no-daemon :app:assembleDebug
```

APK de depuración:

`app/build/outputs/apk/debug/app-debug.apk`

## Compilar con GitHub Actions

1. Sube el contenido de esta carpeta a un repositorio GitHub.
2. Entra en **Actions**.
3. Ejecuta el workflow **Build Android APK** o haz un push a `main` / `master`.
4. Abre la ejecución completada y descarga el artefacto `TraductorPersonal-0.4-debug`.

El workflow usa únicamente acciones públicas y no necesita secretos ni claves API.

## Uso

1. Selecciona el idioma de la otra persona.
2. Pulsa **Escuchar a la otra persona**. El reconocedor de Android intentará transcribir usando el idioma seleccionado; ML Kit identifica el idioma del texto y lo traduce al español.
3. Pulsa **Hablar en español** para dictar en español y traducir al idioma seleccionado.
4. También puedes escribir en el cuadro de texto y usar uno de los dos botones de traducción.
5. Pulsa **Escuchar traducción** para reproducir el resultado.

## Importante: gratuidad y privacidad

- El código no incorpora claves API, suscripciones ni servicios de pago.
- ML Kit Translation procesa la traducción en el dispositivo una vez descargado el modelo.
- La descarga inicial de modelos requiere Internet.
- El reconocimiento de voz de Android **no garantiza funcionamiento offline**: depende del motor de reconocimiento instalado (por ejemplo, el proveedor configurado en el teléfono) y de los idiomas disponibles.
- TextToSpeech depende de las voces instaladas en Android; pueden necesitar descarga.
- El uso de `RecognizerIntent` puede enviar audio al proveedor de reconocimiento configurado por Android. Esta aplicación no controla ese proveedor.
- “Gratis” significa que este proyecto no integra una API de pago ni genera cargos propios; el proveedor de Internet o servicios externos del dispositivo pueden aplicar sus propias condiciones.

## Limitaciones conocidas de esta versión 0.4

- El reconocimiento de voz se realiza por turnos mediante la interfaz de reconocimiento del sistema, no es escucha continua ni manos libres.
- Para una detección de idioma más fiable, dicta una frase completa; textos muy cortos pueden ser ambiguos.
- La detección automática identifica el idioma del texto reconocido, pero la captura de voz usa inicialmente el idioma seleccionado en la lista. Para hablar en un idioma distinto del seleccionado, cambia primero el idioma.
- La lista de idiomas visibles es una selección habitual; la disponibilidad real depende de los idiomas admitidos por ML Kit, del reconocedor y de las voces instaladas.
- Esta entrega incluye configuración para compilar el APK debug. No incluye APK ya compilada ni firma de distribución.

## Versionado

- Nombre: Traductor Personal
- Versión: 0.4
- `versionCode`: 4
- `versionName`: 0.4
