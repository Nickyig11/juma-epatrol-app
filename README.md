
***

# 🚀 ePatrol (Juma): Asistente Inteligente para Patrullas Policiales

## Descripción General

Como desarrollador de este proyecto, he creado ePatrol, una innovadora aplicación móvil diseñada para transformar la eficiencia y la operativa diaria de los agentes policiales en vehículos patrulla. Al integrar funcionalidades avanzadas como la gestión de formularios inteligentes asistida por IA, el control de hardware del vehículo y la generación automática de documentos, ePatrol se posiciona como una herramienta indispensable que he desarrollado para optimizar los procedimientos, reducir la carga administrativa y permitir a los agentes centrarse en lo más importante: su labor en la calle.

## ✨ Características Principales Desarrolladas

He implementado las siguientes características clave en ePatrol:

*   **Lanzador de Aplicaciones Personalizado:** Un acceso rápido y seguro a herramientas esenciales, integrado directamente en la interfaz.
*   **Control Integrado del Vehículo:** Gestión intuitiva de luces y otros sistemas del coche patrulla, con una interfaz clara y funcional.
*   **Gestión de Formularios Inteligentes con IA:**
    *   He desarrollado el autocompletado y campos predefinidos para agilizar la entrada de datos.
    *   La aplicación permite la transcripción de voz a texto para formularios (denuncias, informes, etc.), lo que minimiza la interacción manual.
    *   Integré asistencia de IA (Gemini) para interpretar y estructurar la información verbal, transformando el lenguaje natural en datos estructurados para los formularios.
*   **Generación Automática de Documentos:** He diseñado el sistema para la creación instantánea de archivos DOCX a partir de los datos recopilados en los formularios, eliminando la necesidad de redacción manual.
*   **Grabación de Audio Integrada:** Funcionalidad para la captura y gestión de pruebas sonoras con facilidad, directamente desde la aplicación.
*   **Firma Digital en Pantalla:** Implementé la capacidad de recolectar firmas de forma rápida y segura en el propio dispositivo.
*   **Comunicación Segura con el Servidor:** Desarrollé los mecanismos para el envío eficiente y seguro de datos, audio y documentos generados a un servidor backend.
*   **Modo Noche:** Incluí una interfaz optimizada para condiciones de baja luz, mejorando la visibilidad y reduciendo la fatiga visual de los agentes.

## 📱 Visión General de la Aplicación (UI/UX)

He puesto un énfasis especial en el diseño de una interfaz de usuario clara e intuitiva, buscando que sea accesible y funcional en el entorno exigente de una patrulla.

### Pantalla Principal (HomeFragment)

El punto de partida de la aplicación, que ofrece acceso rápido a las principales funcionalidades. He diseñado esta pantalla para ser el centro de control.
<img width="1073" height="620" alt="image" src="https://github.com/user-attachments/assets/db2e7e49-554d-4330-a14b-743eaf91cabc" />

### Lanzador de Aplicaciones (AppsFragment)

He creado una sección dedicada a organizar y lanzar otras aplicaciones esenciales para el trabajo policial, garantizando que todo esté al alcance de la mano.
<img width="1078" height="619" alt="image" src="https://github.com/user-attachments/assets/a8a62afe-6a98-4a10-a1f2-000c087b5fc8" />

### Control de Luces (LucesFragment)

Desarrollé esta interfaz para permitir el control directo de las luces del vehículo patrulla, una función crítica para la seguridad y la operativa.

<img width="1079" height="631" alt="image" src="https://github.com/user-attachments/assets/27708cbe-809c-4ba7-be7a-90df17c768f2" />

### Formularios Inteligentes (FormulariosFragment / DenunciaFragment)

Un ejemplo de cómo he diseñado los formularios para beneficiarse del autocompletado y la interacción inteligente, incluyendo la entrada de voz.
<img width="1077" height="618" alt="image" src="https://github.com/user-attachments/assets/ba3050dd-6d91-4a42-a9c6-735649a1c5f8" />

### Radio Conmunicación (RadioFragment)

Este fragment tiene un botón central que lleva a una aplicacion de comunicación radio.
<img width="1076" height="618" alt="image" src="https://github.com/user-attachments/assets/fac3fea0-ac67-4cf4-a64b-4626bc7fde35" />



### Firma Digital (SignatureActivity)

He implementado una pantalla dedicada donde los usuarios pueden firmar directamente en el dispositivo, lo que agiliza los procesos que requieren consentimiento o verificación.

<img width="823" height="609" alt="image" src="https://github.com/user-attachments/assets/4c6ae9fe-c016-4384-989a-8054c3f08fbd" />




## ⚙️ Arquitectura y Lógica del Proyecto

He construido ePatrol sobre una arquitectura modular y robusta para garantizar escalabilidad, mantenibilidad y un rendimiento óptimo, aspectos fundamentales en el desarrollo de software.

### Estructura Modular

El proyecto está organizado en módulos lógicos que he diseñado para encapsular funcionalidades específicas, facilitando así el desarrollo y la gestión del código:

*   **Docx:** Encargado de toda la lógica para la generación y conversión de documentos Word.
*   **Formularys:** Gestiona la lógica y la interfaz de usuario para todos los formularios de la aplicación.
*   **RecordAudio:** Implementa la funcionalidad para la grabación y procesamiento de audio.
*   **SendToServer:** Módulo que he desarrollado para manejar toda la comunicación con el backend para el envío de datos.
*   **Signature:** Contiene la implementación de la captura de firmas digitales en pantalla.
*   **Fragments:** Son los contenedores que he utilizado para las distintas vistas y lógicas de la interfaz de usuario.

### Navegación y UI

He gestionado la navegación dentro de la aplicación de manera eficiente utilizando el Android Jetpack Navigation Component.

*   **`nav_graph.xml`**: Yo mismo he definido el flujo de navegación entre los diferentes *fragments* de la aplicación.
*   **`MainActivity`**: Esta actividad actúa como el *host* principal para la navegación. La he configurado para contener el `NavHostFragment` y gestionar la barra de navegación inferior (`BottomNavigationView`).
*   **Fragments**: Cada pantalla o sección de la aplicación (e.g., `HomeFragment`, `AppsFragment`, `LucesFragment`, `DenunciaFragment`) es un *Fragment*. Este enfoque que he adoptado permite una UI dinámica y reutilizable.

### Flujo de Datos (Ejemplos de Mi Implementación)

#### Flujo de Denuncia Asistida por IA

1.  **Entrada de Datos:** He diseñado el `DenunciaFragment` para que el agente interactúe directamente con él.
2.  **Transcripción de Voz:** La funcionalidad de grabación de audio que implementé captura la voz, que luego se transcribe a texto.
3.  **Procesamiento Inteligente:** El texto se envía a un servidor (`transcriber.py`), donde he configurado que utilice Google Speech-to-Text para la transcripción y, posteriormente, el modelo Gemini (`form_filler_gemini.py`) que he integrado para extraer y estructurar los datos relevantes del formulario (e.g., `DenunciaData`).
4.  **Generación de Documento:** Los datos estructurados son utilizados por el `DocxGenerator` que creé para generar automáticamente un documento Word.
5.  **Envío al Servidor:** Finalmente, el documento generado se envía a través del `DocxConverterClient` que he implementado para la comunicación con el backend.

<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/777d359c-7500-4e63-a570-37179a1eea53" />




#### Flujo de Grabación de Audio

1.  **Inicio de Grabación:** He implementado la interfaz de usuario para que el agente inicie la grabación desde la UI dedicada (`RecordAudio` UI).
2.  **Captura de Audio:** El `AudioRecorderManager` que he desarrollado gestiona la captura y el almacenamiento del archivo de audio.
3.  **Carga al Servidor:** El archivo de audio se sube al servidor utilizando el `AudioUploader` que también he implementado.

### Back-End y Servicios Inteligentes

El servidor juega un papel crucial en el procesamiento de la información, especialmente en lo que respecta a la inteligencia artificial y la generación de documentos. Aquí un fragmento del código que he desarrollado para el `transcriber.py`:

```python
# Archivo: transcriber.py
import logging
from google.cloud import speech
from google.oauth2 import service_account
import form_filler_gemini # Módulo para la IA de llenado de formularios

# La ruta a tus credenciales de Google Cloud
KEY_FILE_PATH = '/home/nickyjuma6258/serverSpeach/keys/brave-server-467006-e1-30d8dab5fca1.json'
# Constantes para la transcripción
LANGUAGE_CODE = "es-ES"
SAMPLE_RATE = 44100
EXPECTED_ENCODING = speech.RecognitionConfig.AudioEncoding.LINEAR16

# --- Configuración de Logging ---
# Configuramos un logger específico para este módulo
logging.basicConfig(level=logging.INFO, format='%(asctime)s - %(levelname)s - TRANSCRIBER - %(message)s')
logger = logging.getLogger(__name__)


def process_audio_in_memory(audio_bytes):
    """
    Toma los bytes de un archivo de audio, transcribe y llama al llenador de formulario,
    todo en memoria. Devuelve una tupla (success, result_or_error).
    'result_or_error' será un diccionario si hay éxito, o un string de error si falla.
    """
    logger.info("Iniciando proceso de audio en memoria...")

    # 1. Configurar cliente de Google Speech-to-Text
    try:
        credentials = service_account.Credentials.from_service_account_file(KEY_FILE_PATH)
        client = speech.SpeechClient(credentials=credentials)
    except Exception as e:
        logger.error(f"Error al cargar credenciales de Speech-to-Text: {e}")
        return False, f"Error de credenciales Speech-to-Text: {e}"

    # 2. Preparar el audio y la configuración para la API
    audio = speech.RecognitionAudio(content=audio_bytes)
    config = speech.RecognitionConfig(
        encoding=EXPECTED_ENCODING,
        sample_rate_hertz=SAMPLE_RATE,
        language_code=LANGUAGE_CODE
    )

    # 3. Realizar la transcripción
    logger.info("Enviando audio a la API de Speech-to-Text...")
    full_transcription = ""
    try:
        response = client.recognize(config=config, audio=audio)
        if not response.results:
            logger.warning("No se obtuvieron resultados de la transcripción.")
            full_transcription = "No se obtuvieron resultados de la transcripción." # Texto por defecto para que Gemini sepa que no hay nada
        else:
            # Concatenar todos los resultados de la transcripción
            for result in response.results:
                full_transcription += result.alternatives[0].transcript + "\n"
            full_transcription = full_transcription.strip()
            logger.info("Transcripción obtenida exitosamente en memoria.")

    except Exception as e:
        logger.error(f"Error durante la llamada a la API de transcripción: {e}")
        return False, f"Error en API Speech-to-Text: {e}"

    # 4. Llamar a Gemini para el llenado del formulario
    logger.info("Invocando llenador de formulario (Gemini) en memoria...")

    # Verificaciones de la configuración de Gemini (esto es opcional pero bueno para la depuración)
    if not form_filler_gemini.CONFIG_LOADED_SUCCESSFULLY:
         error_msg = "form_filler_gemini.py no pudo cargar su config de campos (form_fields_config.json)."
         logger.error(error_msg)
         return False, error_msg

    if not form_filler_gemini.GEMINI_API_KEY or form_filler_gemini.GEMINI_API_KEY == form_filler_gemini.PLACEHOLDER_API_KEY:
        error_msg = "La API Key de Gemini no está configurada en form_filler_gemini.py o .env."
        logger.error(error_msg)
        return False, error_msg

    # LLAMADA A LA FUNCIÓN OPTIMIZADA EN MEMORIA DE form_filler_gemini.py
    json_response_dict = form_filler_gemini.fill_form_from_text(full_transcription)

    # 5. Devolver el resultado
    if json_response_dict is not None:
        logger.info("Llenado de formulario completado por Gemini. Devolviendo diccionario al servidor.")
        # Devolvemos True y el diccionario Python
        return True, json_response_dict
    else:
        error_msg = "El módulo de llenado de formulario (Gemini) falló y no devolvió datos."
        logger.error(error_msg)
        return False, error_msg

# El bloque `if __name__ == "__main__":` se elimina porque este módulo
# ya no está pensado para ser ejecutado directamente, sino para ser
# importado y utilizado por `extractServer.py`.
```



### Tecnologías Utilizadas

En el desarrollo de ePatrol, he empleado las siguientes tecnologías clave:

*   **Kotlin:** El lenguaje principal para el desarrollo de la aplicación Android, elegido por su modernidad, seguridad y concisión.
*   **Android SDK:** El conjunto de herramientas esenciales para construir la aplicación en la plataforma Android.
*   **Android Jetpack Navigation Component:** Fundamental para la gestión de la navegación y la arquitectura modular de la UI.
*   **Google Cloud Speech-to-Text API:** Para la potente y precisa transcripción de audio a texto.
*   **Google Gemini API:** Integrado para el procesamiento inteligente del lenguaje natural y el llenado automático de formularios.
*   **Python:** Utilizado en el backend para orquestar la transcripción, el procesamiento con IA y la comunicación con la aplicación.
*   **`python-docx` (librería):** Empleada en el servidor para la generación dinámica de documentos Word.
*   **(Mencionar cualquier otra librería o framework importante si la recuerdas, como Room, Retrofit, etc.)**

## 💡 Conclusión y Futuras Mejoras

Como creador de ePatrol, estoy convencido de que esta aplicación representa un salto significativo en la digitalización y optimización de las operaciones policiales. He logrado desarrollar una herramienta que no solo mejora la eficiencia de los agentes de Juma, sino que también establece un precedente para futuras innovaciones en el sector.

Mis planes a futuro para ePatrol incluyen:

*   **Integración de más hardware:** Expandir el control a otros sistemas del vehículo patrulla.
*   **Análisis predictivo:** Utilizar la IA para ofrecer información relevante en tiempo real basada en datos históricos.
*   **Módulos de entrenamiento interactivos:** Herramientas de capacitación integradas para nuevos agentes.
*   **Mejoras en la accesibilidad:** Continuar optimizando la interfaz para diversas condiciones y usuarios.

Este proyecto demuestra mi capacidad para desarrollar soluciones tecnológicas complejas y de alto impacto, combinando robustez técnica con una profunda comprensión de las necesidades del usuario.

## 👨‍💻 Autor

*   [Nicky Chinedu]



