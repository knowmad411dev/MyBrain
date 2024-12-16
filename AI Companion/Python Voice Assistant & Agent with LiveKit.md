---
tags:
- agents
- speech
- python
---

### How-To Instructions to Build Your Own Voice Assistant Using LiveKit and OpenAI

In this tutorial, you will learn how to create your own version of OpenAI's voice assistant mode. This voice assistant can respond to queries, interact with various Python functions, and even manage smart home tasks like controlling room temperatures.

#### Prerequisites and Tools Required

1. **LiveKit Account**: Used to manage low-latency data transmission for voice and video streaming. You can use either their cloud-hosted solution or deploy your own server.
2. **Python**: Programming language for implementing the assistant.
3. **OpenAI API Key**: Needed to interact with OpenAI's language model.
4. **VSCode**: Preferred IDE for development.

#### Step 1: Set Up Your Virtual Environment

1. **Create a Virtual Environment**:

    ```bash
    python3 -m venv ai
    ```

    (If you are on Windows, you can replace `python3` with `python`).

2. **Activate the Virtual Environment**:

    - On Mac/Linux:

        ```bash
        source ai/bin/activate
        ```

    - On Windows (PowerShell):

        ```powershell
        .\ai\Scripts\Activate.ps1
        ```

    - On Windows (cmd):

        ```bash
        .\ai\Scripts\activate.bat
        ```

#### Step 2: Install Dependencies

To install the required packages, run the following command:

```bash
pip install livekit-agents livekit-plugins openai python-dotenv celerio
```

These packages include:

- **livekit-agents**: To manage interactions with LiveKit.
- **livekit-plugins**: To add capabilities such as speech-to-text and text-to-speech.
- **openai**: Required to connect to OpenAI’s API.
- **python-dotenv**: To manage environment variables.
- **celerio**: Used for voice activity detection.

#### Step 3: Set Up Files

In VSCode or your favorite IDE, create the following files:

- **.env**: To store environment variables such as API keys.
- **main.py**: The main script where the chatbot code will be written.
- **api.py**: A separate script where agent functionalities are implemented.

#### Step 4: Configure Environment Variables

In the `.env` file, set the following variables:

- **LIVEKIT_URL**: WebSocket URL provided by LiveKit.
- **LIVEKIT_API_SECRET**: API secret generated from your LiveKit dashboard.
- **LIVEKIT_API_KEY**: API key generated from your LiveKit dashboard.
- **OPENAI_API_KEY**: API key obtained from OpenAI's platform.

Example `.env` file:

```bash
LIVEKIT_URL="wss://your_livekit_url_here"
LIVEKIT_API_SECRET="your_api_secret_here"
LIVEKIT_API_KEY="your_api_key_here"
OPENAI_API_KEY="your_openai_api_key_here"
```

#### Step 5: Write the Main Script (`main.py`)

The main script contains the basic functionality to connect to LiveKit, set up the assistant, and start interacting.

```python
import asyncio
from dotenv import load_dotenv
from livekit.agents import auto_subscribe, job_context, worker_options, cli
from livekit.agents.voice_assistant import VoiceAssistant
from livekit.plugins import OpenAI, Celerio

load_dotenv()  # Load environment variables

async def entrypoint(ct):
    # Set the context for the AI
    initial_ct = OpenAI.chat_context.append(role="system", text="You are a voice assistant created by LiveKit. Your interface with users will be voice. You should use short and concise responses.")

    # Connect to LiveKit
    await ct.connect(auto_subscribe=auto_subscribe.audio_only)

    # Define the assistant
    assistant = VoiceAssistant(
        vad=Celerio.vad(),  # Voice Activity Detection
        st=OpenAI.st(),     # Speech-to-Text
        lm=OpenAI.LM(),     # Language Model
        tts=OpenAI.tts(),   # Text-to-Speech
        chat_ct=initial_ct
    )

    # Start assistant in the room
    assistant.start(ct.room)

    # Initial prompt
    await asyncio.sleep(1)
    await assistant.say("Hey, how can I help you today?")
    assistant.set(allow_interruptions=True)

if __name__ == "__main__":
    cli.run_app(worker_options(entrypoint_func=entrypoint))
```

This script will create a simple voice assistant, connect it to LiveKit, and provide a greeting prompt. The AI listens to voice inputs, converts them to text, sends them to OpenAI, and responds with synthesized speech.

#### Step 6: Add Custom Agent Functionalities (`api.py`)

To extend your AI assistant, you can add custom functionality. For example, let’s create an agent that can control room temperatures.

```python
import enum
from typing import Annotated
from livekit.agents import LM
import logging

logger = logging.getLogger("temperature_control")
logger.setLevel(logging.INFO)

# Define zones with an enum class
class Zone(enum.Enum):
    living_room = "living_room"
    bedroom = "bedroom"
    kitchen = "kitchen"
    bathroom = "bathroom"
    office = "office"

# Define assistant functions class
class AssistantFunction(LM.function_context):
    def __init__(self):
        super().__init__()
        self._temperature = {
            Zone.living_room: 22,
            Zone.bedroom: 20,
            Zone.kitchen: 24,
            Zone.bathroom: 23,
            Zone.office: 21,
        }

    @LM.ai_callable(description="Get the temperature in a specific room.")
    def get_temperature(self, zone: Annotated[Zone, LM.type_info(description="The specific room.")]):
        logger.info("Get temp - Zone: %s", zone)
        temp = self._temperature[zone]
        return f"The temperature in the {zone.value} is {temp}C."

    @LM.ai_callable(description="Set the temperature in a specific room.")
    def set_temperature(self, zone: Annotated[Zone, LM.type_info(description="The specific room.")], temp: Annotated[int, LM.type_info(description="The temperature to set.")]):
        logger.info("Set temp - Zone: %s, Temp: %s", zone, temp)
        self._temperature[zone] = temp
        return f"The temperature in the {zone.value} is now {temp}C."
```

This script creates a `Zone` enum for different areas of the house and an `AssistantFunction` class to interact with the temperature in those zones. You can extend this to add more functionalities, such as controlling lights or interacting with other smart devices.

#### Step 7: Integrate Custom Functionalities with Main Script

Import the `AssistantFunction` into your `main.py` script and integrate it with your assistant:

```python
from api import AssistantFunction

# Add custom agent functionality
fac_ct = AssistantFunction()
assistant = VoiceAssistant(
    vad=Celerio.vad(),
    st=OpenAI.st(),
    lm=OpenAI.LM(),
    tts=OpenAI.tts(),
    chat_ct=initial_ct,
    fac_ct=fac_ct
)
```

#### Step 8: Testing Your Voice Assistant

To run the agent, use:

```bash
python main.py start
```

Then use the hosted playground provided by LiveKit to interact with your agent.

1. **Log in to LiveKit** and connect to the project you created.
2. **Use the Web Playground** to test voice interaction.
3. **Ask Questions** like, "What's the temperature in the bedroom?" or "Set the temperature in the living room to 24 degrees." Your assistant should respond appropriately.

[[AI Companion]]  [[AI Voice Assistants]]  [[Python]]  [[OpenAI]]