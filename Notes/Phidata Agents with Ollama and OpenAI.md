---
tags:
- ollama
- openai
- automation
- python
video-url: https://www.youtube.com/watch?v=geHPlAJanVE&list=WL&index=1
---

## **Phidata Agents with Ollama and OpenAI

### Introduction

Phidata Agents represent a powerful way to create customized AI workflows by combining the capabilities of Ollama and OpenAI. With these agents, you can easily set up conversational AI applications, automate complex processes, and create intelligent assistants that integrate seamlessly with other services. This overview will cover what Phidata Agents are, their architecture, and how to get started with Ollama and OpenAI to build your own agents.

### Overview of Phidata Agents

Phidata Agents are modular, scalable AI components designed to enable a wide range of tasks, from natural language processing to automation. They leverage the strengths of two key AI tools:

1. **Ollama**: A platform for managing large language models (LLMs) like Llama 2, and other fine-tuned models locally or in the cloud.
2. **OpenAI**: Provides robust LLM capabilities, such as GPT-4, to create context-aware, dynamic responses and handle a wide array of conversational scenarios.

### Key Components

- **Agent Framework**: The agent framework uses models from Ollama or OpenAI as back-end LLMs, allowing for the efficient generation of responses, decision-making, and integration with APIs.
- **Task Handling**: Tasks can be handled by the agent, whether they involve conversing with users, providing recommendations, or performing actions based on API calls.
- **Communication Layer**: Agents can communicate with third-party services to gather data or perform actions, making them extensible for a wide variety of use cases.

### How to Set Up Phidata Agents with Ollama and OpenAI

Below is a step-by-step guide to create your own Phidata Agent using Ollama and OpenAI.

#### Prerequisites

- **Python 3.8 or later** installed.
- **Ollama CLI** installed to manage LLMs locally. You can download it from the [Ollama website](https://ollama.com/).
- **OpenAI API key**: You will need an API key from OpenAI to access their models. You can get it from the [OpenAI API page](https://platform.openai.com/signup/).
- **Phidata Python SDK** installed. You can install it using pip:
  ```bash
  pip install phidata
  ```

#### Step 1: Set Up the Environment

Create a virtual environment to keep dependencies isolated and manageable:

```bash
python -m venv phidata_env
source phidata_env/bin/activate   # On Windows, use `phidata_env\Scripts\activate`
```

Install the necessary Python packages:

```bash
pip install phidata openai requests
```

#### Step 2: Configure the Agent

First, create a configuration file (e.g., `config.py`) to set up the necessary keys and endpoints for Ollama and OpenAI. Here is an example:

```python
# config.py

OLLAMA_API_URL = "http://localhost:11400"  # Default Ollama endpoint
OPENAI_API_KEY = "your_openai_api_key"

MODEL_NAME = "llama2"  # Ollama model to use
```

#### Step 3: Create the Phidata Agent

Below is an example Python script (`agent.py`) to create a Phidata Agent using Ollama and OpenAI:

```python
import openai
import requests
from config import OLLAMA_API_URL, OPENAI_API_KEY, MODEL_NAME

class PhidataAgent:
    def __init__(self, model_name, ollama_api_url, openai_api_key):
        self.model_name = model_name
        self.ollama_api_url = ollama_api_url
        self.openai_api_key = openai_api_key

    def ask_ollama(self, prompt):
        response = requests.post(
            f"{self.ollama_api_url}/api/generate",
            json={"model": self.model_name, "prompt": prompt}
        )
        if response.status_code == 200:
            return response.json().get("text", "")
        else:
            return f"Error: {response.status_code}"

    def ask_openai(self, prompt):
        openai.api_key = self.openai_api_key
        response = openai.Completion.create(
            engine="davinci",
            prompt=prompt,
            max_tokens=150
        )
        return response.choices[0].text.strip()

    def respond(self, prompt):
        # First, attempt to get response from Ollama
        ollama_response = self.ask_ollama(prompt)
        if ollama_response:
            return ollama_response

        # Fallback to OpenAI if Ollama fails
        return self.ask_openai(prompt)

# Usage example
if __name__ == "__main__":
    agent = PhidataAgent(MODEL_NAME, OLLAMA_API_URL, OPENAI_API_KEY)
    user_input = "Tell me about the benefits of using Phidata Agents."
    response = agent.respond(user_input)
    print("Agent Response:", response)
```

### Step 4: Running the Agent

To run the agent, simply execute the `agent.py` script in your terminal:

```bash
python agent.py
```

You should see the agent’s response based on the models specified. It will first attempt to get a response from Ollama, and if Ollama doesn’t provide a response, it will use OpenAI as a fallback.

### Step 5: Customizing the Agent

- **Add New Features**: You can extend the `PhidataAgent` class to add more complex features such as conversation history or external API integrations.
- **Conversation Context**: Keep track of user inputs and responses to provide a conversational experience. You can achieve this by storing previous inputs in a list and appending each new user query to maintain context.

### Example: Adding Context to the Agent

Here's how you could add a conversation history to the agent:

```python
class PhidataAgentWithContext(PhidataAgent):
    def __init__(self, model_name, ollama_api_url, openai_api_key):
        super().__init__(model_name, ollama_api_url, openai_api_key)
        self.conversation_history = []

    def respond(self, prompt):
        self.conversation_history.append({"role": "user", "content": prompt})
        context = "\n".join([f"{msg['role']}: {msg['content']}" for msg in self.conversation_history])
        response = super().respond(context)
        self.conversation_history.append({"role": "agent", "content": response})
        return response

# Usage example
if __name__ == "__main__":
    agent = PhidataAgentWithContext(MODEL_NAME, OLLAMA_API_URL, OPENAI_API_KEY)
    user_input = "What is Ollama?"
    response = agent.respond(user_input)
    print("Agent Response:", response)
```

### Conclusion

Phidata Agents provide a robust framework to leverage the power of both Ollama and OpenAI for building intelligent, conversational AI systems. With Ollama for local model management and OpenAI for advanced language processing, you can create versatile agents capable of performing complex tasks. The modular nature of Phidata Agents allows for easy customization, making them a great choice for anyone looking to enhance their automation capabilities or develop personalized AI assistants.

[[Ollama]]    [[Python]]  [[Workflow]]