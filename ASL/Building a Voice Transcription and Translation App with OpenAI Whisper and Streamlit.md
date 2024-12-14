---
tags:
- python
- speech
---

## **Building a Voice Transcription and Translation App with OpenAI Whisper and Streamlit**

This guide will teach you how to use the Streamlit `st.audio_input` widget to record your voice on your device microphone, paired with the OpenAI Whisper model to transcribe and/or translate your speech to text in English. You can later download the transcribed content as a text file in the `.txt` format.

## Prerequisites

- Basic [Python](https://www.python.org/downloads/) knowledge
- [Streamlit](https://docs.streamlit.io/)
- [[OpenAI]] API key. [Sign up](https://platform.openai.com/signup) for an account

## What is Whisper

Whisper is a trained open-source neural network that approaches human-level robustness and accuracy in English speech recognition.

The OpenAI API provides two endpoints:

- Transcriptions
- Translations

## What is Streamlit

From the [official website](https://streamlit.io/), Streamlit is a faster way to build and share data apps. It is an open-source Python library that helps you build web applications for sharing analytical results, building complex interactive experiences, and iterating on top of new machine-learning models.

## Installing Streamlit

To run any Streamlit apps, you must first install Streamlit using the command:

```bash
pip install streamlit
```

## Installing Other Libraries

Since we are working with transforming audio to text, we need to store our environment variables securely:

```bash
pip install openai python-dotenv
```

## Creating the Environment Variable

Create a new file in the root project directory and name it `.env`.

Paste in your OpenAI [API key](https://platform.openai.com/settings/profile?tab=api-keys):

`.env`

```plaintext
OPENAI_API_KEY=your_openai_api_key_here
```

## Creating the App

In your directory, create this file, `streamlit_app.py`, which will contain all the Python code to transcribe and translate our audio and output the resulting text.

To initialize an instance of the OpenAI client, copy-paste this code:

`streamlit_app.py`

```python
import os
from dotenv import load_dotenv
import openai

load_dotenv()

api_key = os.getenv('OPENAI_API_KEY')
client = openai
```

The code block connects and reads our secret key in the `.env` file, making sure we are authenticated as users.

PS: Using the OpenAI API is not free as you have to buy some credits to use the service.

## Transcription with Whisper

Let's update the `streamlit_app.py` with the following:

`streamlit_app.py`

```python
import streamlit as st

st.title("Transcription with Whisper")

audio_value = st.audio_input("Record a voice message to transcribe")

if audio_value:
    transcript = client.Audio.transcriptions.create(
        model="whisper-1",
        file=audio_value
    )
    transcript_text = transcript['text']
    st.write(transcript_text)
```

The [transcriptions API](https://platform.openai.com/docs/guides/speech-to-text#transcriptions) will convert our audio using the `st.audio_input` widget to record our voice. If the recording exists, the Whisper model is used to create the desired file format for the transcription of the audio and output the text using the `st.write()` function, which takes a string and writes it directly into our web app.

To use the exact logo at the top left of the app, [download this](https://github.com/Terieyenike/streamlit_audio/blob/main/logo.png) and save it in your project directory.

Now, let's run this app with this command in the terminal:

```bash
streamlit run streamlit_app.py
```

## Downloading the Transcribed Text

The ability to download the transcribed message for later serves for record-keeping when you need it.

Streamlit offers an input widget that allows for the display of a download button. Update the `streamlit_app.py` file with the following code:

```python
txt_file = "transcription.txt"

# Initialize session state for download confirmation
if "downloaded" not in st.session_state:
    st.session_state.downloaded = False

# Download button
if st.download_button(
    label="Download Transcription",
    file_name=txt_file,
    data=transcript_text,
):
    st.session_state.downloaded = True

# Show success message after download
if st.session_state.downloaded:
    st.success("Transcription file downloaded successfully!")
```

The following occurs in the lines of code above:

- `st.session_state` in Streamlit allows you to share variables between reruns, for each user session.
- The `transcript_text` variable will contain the content of the transcribed text.
- The `txt_file` variable with the assigned value, `transcription.txt`, is the file name of the transcribed text when the file is downloaded.
- Within the function of the `st.download_button()`, the label describes to the user what the button is for.

## Translation with Whisper

The process of creating the translation is similar to creating the transcription. The [translation endpoint](https://platform.openai.com/docs/guides/speech-to-text#translations) will translate a foreign language into written text in English from the input of the audio file.

Copy and paste this code.

`streamlit_app.py`

```python
st.header("Translation with Whisper")

audio_translate = st.audio_input("Record a voice message to translate")

if audio_translate:
    translate = client.Audio.translations.create(
        model="whisper-1",
        file=audio_translate
    )
    st.write(translate['text'])
```

If you want to create a file to save your translated audio file as text, you can do the same as with the **Download transcription** button.

The complete source code is [in this repository](https://github.com/Terieyenike/streamlit_audio), and you can [try the app here](https://your-voice.streamlit.app/) to transcribe and translate your voice to text.

Good luck!

## Conclusion

Instead of using pre-recorded audio from the internet as seen in the [OpenAI docs](https://platform.openai.com/docs/guides/speech-to-text), Streamlit offers you the opportunity to use your voice and pair it with the transcription and translation endpoints provided by OpenAI to create this outstanding project.

The microphone in your device can do so much, as technology has made it possible to go beyond using it for communication during meetings and calls.

[[Python]]  [[AI Voice Assistants]]  [[OpenAI]]  