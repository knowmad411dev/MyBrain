---
tags:
- openai
- ollama
- python
video-url: https://www.youtube.com/watch?v=8jpVeUTNExI
---

## **Overview of Ollama + OpenAI Swarm Integration**

OpenAI recently released an experimental tool called Swarm, which allows you to create a group of AI agents that collaborate to solve complex tasks. By default, Swarm uses OpenAI models like GPT-4, which can be costly due to the token usage involved. However, it is possible to use Ollama, a locally-hosted LLM, to power Swarm agents. This guide will walk you through modifying Swarm to work with Ollama, allowing you to run AI agents on your local machine, completely free of charge.

**Why Use Ollama with Swarm?**

- **Cost-Effective**: Swarm with GPT can become expensive quickly, especially for function-calling applications that require many tokens. With Ollama, you can run the agents for free, using local resources.
- **Flexibility**: Ollama supports function calling with the same format as OpenAI models, meaning it is easy to integrate with Swarm.
- **Diverse Models**: Ollama allows you to use different models for different agents, unlike OpenAI which offers limited options for agents.

**Step-by-Step Guide to Integrate Ollama with Swarm**

1. **Prerequisites**
   - Ensure you have Python and Git installed on your computer.
   - Install Ollama by visiting [ollama.com](https://ollama.com) and clicking the download button. Ollama supports Windows, macOS, and Linux.
   - Install Swarm from OpenAI's GitHub repository.

2. **Modify Swarm to Work with Ollama**

   To modify Swarm to work with Ollama, you need to change the code to point to Ollama instead of OpenAI's API. Ollama provides OpenAI compatibility by allowing you to override the base URL used by the OpenAI library.

   **Code Changes: Overview**
   - Import the OpenAI library.
   - Set up the chat completion just as you would for GPT, but change the base URL to point to Ollama's local server (default is `http://localhost:11434`).

   **Code Example**
   ```python
   import openai

   # Set up Ollama with OpenAI compatibility
   openai.api_key = "YOUR_API_KEY"  # Ollama doesn't require an API key, but it's still defined for compatibility
   openai.api_base = "http://localhost:11434"  # Change base URL to Ollama's local server

   # Example to create chat completion
   response = openai.ChatCompletion.create(
       model="quenn2-5-coder",  # Specify your preferred model
       messages=[{"role": "user", "content": "Your message here"}]
   )
   print(response["choices"][0]["message"]["content"])
   ``

3. **Instantiate Ollama Client in Swarm Code**
   Modify the Swarm repository's main code to point the OpenAI client to Ollama instead. You will instantiate the Ollama client instead of the default OpenAI client by adding a base URL reference as shown below:

   **Code Change in Swarm's Setup**
   ```python
   import openai

   # Update OpenAI settings to use Ollama as the base URL
   openai.api_key = "YOUR_API_KEY"
   openai.api_base = "http://localhost:11434"

   # Instantiate Swarm with Ollama client
   swarm = Swarm(client=openai)
   swarm_instance = swarm.create_instance(client=openai)  # Pass Ollama client to Swarm
   ``

4. **Configure Environment Variables**
   Create an environment variable file (e.g., `.env`) to store the default model for your agents. Since Ollama does not require an API key, the file only contains the model details. Example:
   ```
   # .env file for Ollama Swarm setup
   LLM_MODEL=quenn2-5-coder
   ```

   Reference the environment variable in your Python script where you instantiate agents:

   ```python
   import os

   model = os.getenv("LLM_MODEL", "quenn2-5-coder")
   ``

5. **Running the Agent Swarm**

   Use the following script to run the agents locally:

   **Run Script (run.py)**
   ```python
   import openai

   # Initialize Swarm with local Ollama models
   openai.api_key = "YOUR_API_KEY"
   openai.api_base = "http://localhost:11434"

   # Swarm setup
   from swarm import Swarm
   client = openai
   swarm_instance = Swarm(client)

   # Create and manage agent swarm
   def run_swarm():
       agent_input = "How many users are currently on the platform?"
       response = swarm_instance.handle_request(agent_input)
       print(response)

   if __name__ == "__main__":
       run_swarm()
   ```

6. **Testing and Deployment**
   - After installing Ollama and modifying the Swarm code as described, you can run the agents by executing `run.py`.
   - Example command:
     ```sh
     python run.py
     ```
   - This will initiate a Swarm with multiple agents that are able to query your database, and each agent will use the local Ollama instance for processing.

7. **Pulling Models for Agents**

   Use Ollama to pull models that support tool calling, which is crucial for agents to interact effectively.

   ```sh
   ollama pull quenn2-5-coder
   ```

   Once the models are pulled, update the environment configuration to reference the correct model.

**Conclusion**

By using Ollama with OpenAI Swarm, you can efficiently create a group of AI agents that operate locally on your computer, free of cost. The flexibility and ease of integration make Ollama a great alternative to GPT-4 when cost and local hosting are concerns. You can use different models for each agent, customize their behavior, and run everything on a personal device.

This setup allows you to create scalable, multi-agent systems without the expenses associated with cloud-based AI, and it also provides a diverse choice of models, empowering you to tailor the agents based on specific needs.

[[Ollama]]  [[OpenAI]]  [[Python]]