---
tags:
- automation
- web
video-url: https://www.youtube.com/watch?v=E2GIZrsDvuM&list=WL&index=3
---
## **Overview of Open WebUI with N8N Agents**

This guide will walk you through integrating **Open WebUI** into the **Local AI Starter Kit** to create a feature-rich, self-hosted AI environment. Using **Open WebUI** allows for a natural chat interface for interacting with local AI models and **n8n** workflows directly, enabling the use of voice interactions and custom functionalities with n8n agents.

**Open WebUI** is an open-source, ChatGPT-like interface used to chat with LLMs (e.g., running with **Ollama**). It also allows extended functionality through features like **functions** and **pipelines**, making it easy to interact with your agents or custom APIs. The **n8n** tool is an open-source workflow automation platform that is ideal for building agent workflows for local AI models.

### Components of the Integration

The integration involves:

- **n8n**: To build agent workflows.
- **Ollama**: To run local language models.
- **Quadrant**: For vector storage for RAG (retrieval-augmented generation).
- **Postgres**: A SQL database to store chat memory for agents.
- **Open WebUI**: An interface to interact with n8n workflows, Ollama models, and use voice chat.

All of these services run in Docker containers orchestrated by **Docker Compose** to create a local AI environment.

### How-To Instructions

#### 1. Setting Up the Local AI Environment

First, clone the repository that includes all the needed components:

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/<your-repo-path>/local-ai-starter-kit-open-webui.git
   cd local-ai-starter-kit-open-webui
   ```
2. **Environment Setup**:
   - Open the `.env.example` file, customize it to your preferences (e.g., database username, password), and rename it to `.env`.
3. **Install Docker**: If you don't have Docker, install Docker Desktop or Docker CLI to proceed.

#### 2. Running the Containers

1. **Compose Docker Containers**: Run the containers using the Docker Compose command:
   ```bash
   docker-compose -f docker-compose.yml up -d --build
   ```

   This will pull and run containers for **Postgres**, **n8n**, **Quadrant**, **Ollama**, and **Open WebUI**.

2. The environment will start all services, each as a separate container. You can monitor their logs to ensure they are up and running:
   ```bash
   docker-compose logs -f
   ```

#### 3. Configuring n8n Workflows

1. **Access n8n UI**: Open n8n in your browser:
   - Navigate to `http://localhost:5678`. You will need to set up a local account (it's just for local authentication).
2. **Create a Workflow**:
   - Use a **Webhook Trigger** to set up an agent workflow in n8n. This webhook will accept incoming requests from Open WebUI to trigger your workflow.
   - Set the URL path for the webhook (e.g., `/invoke_n8n_agent`).
   - Use nodes to connect different parts of your workflow, including connections to **Ollama** (for LLM queries), **Quadrant** (for vector storage), and **Postgres** (for managing memory).
3. **Connect to Ollama and Quadrant**:
   - For **Ollama**: Set up a node to interact with your LLM.
   - For **Quadrant**: Retrieve stored vectors or knowledge base information.
   - Configure credentials directly within n8n by specifying endpoints such as `http://ollama:11434` and `http://quadrant:6333`.

#### 4. Adding Open WebUI to Docker Compose

To integrate **Open WebUI** into the Local AI Starter Kit, edit the `docker-compose.yml` file:

```yaml
  openwebui:
    image: openwebui/openwebui:latest
    container_name: openwebui
    ports:
      - "3000:3000"
    networks:
      - local_ai_network
    depends_on:
      - ollama
```

This snippet will add **Open WebUI** to your Docker setup, exposing it on port `3000`.

#### 5. Using Open WebUI with n8n Workflows

1. **Access Open WebUI**: Open `http://localhost:3000` to access the UI. Create a local account.
2. **Set Up n8n Functions in Open WebUI**: Go to the **Functions** section in Open WebUI:
   - Create a function (a custom Python script) to connect to your n8n agent workflow using the webhook URL you defined (e.g., `http://n8n:5678/invoke_n8n_agent`).
   - **Example Python script** for the function:
     ```python
     import requests
     def run_webhook(session_id, input_prompt):
         url = "http://n8n:5678/invoke_n8n_agent"
         payload = {
             "session_id": session_id,
             "chat_input": input_prompt
         }
         response = requests.post(url, json=payload)
         return response.json()
     ```
3. **Run a Chat Test**: Open a new chat in Open WebUI and select the n8n function to ask questions and see responses coming from the workflow.

#### 6. Using Voice to Interact

Open WebUI also includes a voice interaction feature, allowing you to speak directly to your agents:

- Click the **microphone** icon to initiate voice communication.
- Follow the prompts and speak to your n8n agents as you would in text mode.

#### 7. Advanced Customization

You can extend functionality using **pipelines** within **Open WebUI**, which are similar to functions but allow more complex workflows and integrations:

- Set up new pipelines in Open WebUI to interact with **LangChain**, **Llama Index**, or other AI tools directly from the UI.

### Conclusion

The integration of **Open WebUI** and **n8n** allows for a highly interactive and feature-rich local AI environment. You can manage workflows, interact with LLMs, and even use voice commands, all from a single, cohesive platform.

By using Docker Compose to orchestrate all services, you achieve a powerful, completely local AI setup. This solution gives you privacy, control, and the ability to extend your AI capabilities to meet evolving needs.

[[Open Web UI]]  [[Ollama]]  [[Python]]