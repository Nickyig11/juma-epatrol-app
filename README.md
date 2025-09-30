***

# 🚀 ePatrol (Juma): Intelligent Assistant for Police Patrols

## General Description

As the developer of this project, I have created ePatrol, an innovative mobile application designed to transform the efficiency and daily operations of police officers in patrol vehicles. By integrating advanced functionalities such as AI-assisted smart form management, vehicle hardware control, and automatic document generation, ePatrol stands as an indispensable tool I have developed to optimize procedures, reduce administrative burden, and allow officers to focus on what matters most: their work on the street.

## ✨ Key Features Developed

I have implemented the following key features in ePatrol:

*   **Custom Application Launcher:** Quick and secure access to essential tools, integrated directly into the interface.
*   **Integrated Vehicle Control:** Intuitive management of patrol car lights and other systems, with a clear and functional interface.
*   **Smart Form Management with AI:**
    *   I have developed auto-completion and predefined fields to streamline data entry.
    *   The application allows voice-to-text transcription for forms (complaints, reports, etc.), minimizing manual interaction.
    *   I integrated AI assistance (Gemini) to interpret and structure verbal information, transforming natural language into structured data for forms.
*   **Automatic Document Generation:** I designed the system for instant creation of DOCX files from collected form data, eliminating the need for manual drafting.
*   **Integrated Audio Recording:** Functionality for easy capture and management of sound evidence, directly from the application.
*   **On-Screen Digital Signature:** I implemented the ability to collect signatures quickly and securely on the device itself.
*   **Secure Server Communication:** I developed the mechanisms for efficient and secure transmission of generated data, audio, and documents to a backend server.
*   **Night Mode:** I included an interface optimized for low-light conditions, improving visibility and reducing eye strain for officers.

## 📱 Application Overview (UI/UX)

I have placed special emphasis on designing a clear and intuitive user interface, aiming for it to be accessible and functional in the demanding environment of a patrol.

### Main Screen (HomeFragment)

The starting point of the application, offering quick access to main functionalities. I designed this screen to be the control center.

<img width="1073" height="620" alt="image" src="https://github.com/user-attachments/assets/db2e7e49-554d-4330-a14b-743eaf91cabc" />

### Application Launcher (AppsFragment)

I created a dedicated section to organize and launch other essential applications for police work, ensuring everything is at hand.

<img width="1078" height="619" alt="image" src="https://github.com/user-attachments/assets/a8a62afe-6a98-4a10-a1f2-000c087b5fc8" />

### Light Control (LucesFragment)

I developed this interface to allow direct control of the patrol vehicle's lights, a critical function for safety and operation.

<img width="1079" height="631" alt="image" src="https://github.com/user-attachments/assets/27708cbe-809c-4ba7-be7a-90df17c768f2" />

### Smart Forms (FormulariosFragment / DenunciaFragment)

An example of how I designed the forms to benefit from auto-completion and intelligent interaction, including voice input.

<img width="1077" height="618" alt="image" src="https://github.com/user-attachments/assets/ba3050dd-6d91-4a42-a9c6-735649a1c5f8" />

### Radio Communication (RadioFragment)

This fragment has a central button that leads to a radio communication application.

<img width="1076" height="618" alt="image" src="https://github.com/user-attachments/assets/fac3fea0-ac67-4cf4-a64b-4626bc7fde35" />

### Digital Signature (SignatureActivity)

I implemented a dedicated screen where users can sign directly on the device, streamlining processes that require consent or verification.


<img width="823" height="609" alt="image" src="https://github.com/user-attachments/assets/4c6ae9fe-c016-4384-989a-8054c3f08fbd" />



## ⚙️ Project Architecture and Logic

I have built ePatrol on a modular and robust architecture to ensure scalability, maintainability, and optimal performance, fundamental aspects of software development.

### Modular Structure

The project is organized into logical modules that I designed to encapsulate specific functionalities, thus facilitating development and code management:

*   **Docx:** Responsible for all logic for generating and converting Word documents.
*   **Formularys:** Manages the logic and user interface for all application forms.
*   **RecordAudio:** Implements functionality for audio recording and processing.
*   **SendToServer:** Module I developed to handle all communication with the backend for data transmission.
*   **Signature:** Contains the implementation of on-screen digital signature capture.
*   **Fragments:** These are the containers I used for the different views and logic of the user interface.

### Navigation and UI

I have managed navigation within the application efficiently using the Android Jetpack Navigation Component.

*   **`nav_graph.xml`**: I myself defined the navigation flow between the different *fragments* of the application.
*   **`MainActivity`**: This activity acts as the main *host* for navigation. I configured it to contain the `NavHostFragment` and manage the bottom navigation bar (`BottomNavigationView`).
*   **Fragments**: Each screen or section of the application (e.g., `HomeFragment`, `AppsFragment`, `LucesFragment`, `DenunciaFragment`) is a *Fragment*. This approach I adopted allows for a dynamic and reusable UI.

### Data Flow (Examples of My Implementation)

#### AI-Assisted Complaint Flow

1.  **Data Input:** I designed the `DenunciaFragment` for direct agent interaction.
2.  **Voice Transcription:** The audio recording functionality I implemented captures voice, which is then transcribed into text.
3.  **Intelligent Processing:** The text is sent to a server (`transcriber.py`), where I configured it to use Google Speech-to-Text for transcription and, subsequently, the Gemini model (`form_filler_gemini.py`) that I integrated to extract and structure relevant form data (e.g., `DenunciaData`).
4.  **Document Generation:** The structured data is used by the `DocxGenerator` I created to automatically generate a Word document.
5.  **Server Submission:** Finally, the generated document is sent via the `DocxConverterClient` I implemented for backend communication.



<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/777d359c-7500-4e63-a570-37179a1eea53" />



#### Audio Recording Flow

1.  **Start Recording:** I implemented the user interface for the agent to start recording from the dedicated UI (`RecordAudio` UI).
2.  **Audio Capture:** The `AudioRecorderManager` I developed manages the capture and storage of the audio file.
3.  **Server Upload:** The audio file is uploaded to the server using the `AudioUploader` that I also implemented.

### Back-End and Intelligent Services

The server plays a crucial role in processing information, especially concerning artificial intelligence and document generation. Here is a fragment of the code I developed for `transcriber.py`:

```python
# File: transcriber.py
import logging
from google.cloud import speech
from google.oauth2 import service_account
import form_filler_gemini # Module for AI form filling

# The path to your Google Cloud credentials
KEY_FILE_PATH = '/home/nickyjuma6258/serverSpeach/keys/...'
# Constants for transcription
LANGUAGE_CODE = "es-ES"
SAMPLE_RATE = 44100
EXPECTED_ENCODING = speech.RecognitionConfig.AudioEncoding.LINEAR16

# --- Logging Configuration ---
# Configure a specific logger for this module
logging.basicConfig(level=logging.INFO, format='%(asctime)s - %(levelname)s - TRANSCRIBER - %(message)s')
logger = logging.getLogger(__name__)


def process_audio_in_memory(audio_bytes):
    """
    Takes audio file bytes, transcribes, and calls the form filler,
    all in memory. Returns a tuple (success, result_or_error).
    'result_or_error' will be a dictionary on success, or an error string on failure.
    """
    logger.info("Starting in-memory audio processing...")

    # 1. Configure Google Speech-to-Text client
    try:
        credentials = service_account.Credentials.from_service_account_file(KEY_FILE_PATH)
        client = speech.SpeechClient(credentials=credentials)
    except Exception as e:
        logger.error(f"Error loading Speech-to-Text credentials: {e}")
        return False, f"Speech-to-Text credential error: {e}"

    # 2. Prepare audio and configuration for the API
    audio = speech.RecognitionAudio(content=audio_bytes)
    config = speech.RecognitionConfig(
        encoding=EXPECTED_ENCODING,
        sample_rate_hertz=SAMPLE_RATE,
        language_code=LANGUAGE_CODE
    )

    # 3. Perform transcription
    logger.info("Sending audio to Speech-to-Text API...")
    full_transcription = ""
    try:
        response = client.recognize(config=config, audio=audio)
        if not response.results:
            logger.warning("No transcription results obtained.")
            full_transcription = "No transcription results obtained." # Default text for Gemini to know there's nothing
        else:
            # Concatenate all transcription results
            for result in response.alternatives:
                full_transcription += result.alternatives[0].transcript + "\n"
            full_transcription = full_transcription.strip()
            logger.info("Transcription successfully obtained in memory.")

    except Exception as e:
        logger.error(f"Error during transcription API call: {e}")
        return False, f"Speech-to-Text API error: {e}"

    # 4. Call Gemini for form filling
    logger.info("Invoking form filler (Gemini) in memory...")

    # Gemini configuration checks (optional but good for debugging)
    if not form_filler_gemini.CONFIG_LOADED_SUCCESSFULLY:
         error_msg = "form_filler_gemini.py could not load its field config (form_fields_config.json)."
         logger.error(error_msg)
         return False, error_msg

    if not form_filler_gemini.GEMINI_API_KEY or form_filler_gemini.GEMINI_API_KEY == form_filler_gemini.PLACEHOLDER_API_KEY:
        error_msg = "Gemini API Key is not configured in form_filler_gemini.py or .env."
        logger.error(error_msg)
        return False, error_msg

    # CALL TO THE OPTIMIZED IN-MEMORY FUNCTION OF form_filler_gemini.py
    json_response_dict = form_filler_gemini.fill_form_from_text(full_transcription)

    # 5. Return the result
    if json_response_dict is not None:
        logger.info("Form filling completed by Gemini. Returning dictionary to server.")
        # Return True and the Python dictionary
        return True, json_response_dict
    else:
        error_msg = "The form filling module (Gemini) failed and returned no data."
        logger.error(error_msg)
        return False, error_msg

# The `if __name__ == "__main__":` block is removed because this module
# is no longer intended to be executed directly, but rather to be
# imported and used by `extractServer.py`.
```



### Technologies Used

In the development of ePatrol, I have used the following key technologies:

*   **Kotlin:** The main language for Android application development, chosen for its modernity, safety, and conciseness.
*   **Android SDK:** The essential set of tools for building the application on the Android platform.
*   **Android Jetpack Navigation Component:** Fundamental for managing navigation and the modular UI architecture.
*   **Google Cloud Speech-to-Text API:** For powerful and accurate audio-to-text transcription.
*   **Google Gemini API:** Integrated for intelligent natural language processing and automatic form filling.
*   **Python:** Used in the backend to orchestrate transcription, AI processing, and communication with the application.
*   **`python-docx` (library):** Used on the server for dynamic Word document generation.
*   **(Mention any other important libraries or frameworks if you remember them, such as Room, Retrofit, etc.)**

## 💡 Conclusion and Future Improvements

As the creator of ePatrol, I am convinced that this application represents a significant leap in the digitalization and optimization of police operations. I have managed to develop a tool that not only improves the efficiency of Juma's agents but also sets a precedent for future innovations in the sector.

My future plans for ePatrol include:

*   **Integration of more hardware:** Expanding control to other patrol vehicle systems.
*   **Predictive analytics:** Using AI to offer relevant information in real time based on historical data.
*   **Interactive training modules:** Integrated training tools for new agents.
*   **Accessibility improvements:** Continuing to optimize the interface for various conditions and users.

This project demonstrates my ability to develop complex and high-impact technological solutions, combining technical robustness with a deep understanding of user needs.

## 👨‍💻 Author

*   [Nicky Chinedu]


