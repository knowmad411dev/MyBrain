---
tags:
- llm
- ollama
- automation
video-url: https://www.youtube.com/watch?v=XQ7wNqbB1x8&list=WL&index=1
---
## **The ULTIMATE Local AI Setup - LLMs, Qdrant, n8n

## Overview of Self-Hosted AI Agent Setup

This tutorial walks you through building a self-hosted AI agent using open-source tools like the Quadrant Vector Store (a vector database), multiple large language models with AMA, and Docker to manage dependencies. You will upload documents and interact with them using a chat model, all on your local machine. The process includes:

1. **Cloning and setting up the starter kit repository from GitHub.**
2. **Using Docker** to create and run containers for the AI agent.
3. **Setting up embeddings and language models via AMA.**
4. **Connecting components** like vector storage, embeddings, and chat interfaces.
5. **Testing** the setup to verify correct operation.

### Requirements:

- **Docker installed** on your machine.
- **GitHub account** to clone repositories.
- Familiarity with **running commands** in a terminal.

---

## Step-by-Step Setup Instructions

### Step 1: Clone the GitHub Repository

1. Open your terminal.
2. Clone the repository:
   ```bash
   git clone https://github.com/nn-iio/self-hosted-ai-starter-kit
   ```
3. Navigate into the cloned repository:
   ```bash
   cd self-hosted-ai-starter-kit
   ```

### Step 2: Set Up Docker Containers

Docker is used to set up the necessary services, including AMA models, a Postgres database, and the Quadrant Vector Store.

1. Open Docker Desktop to monitor container setup.
2. Run Docker Compose from the terminal to set up the environment:
   ```bash
   docker-compose -f docker-compose.yml --profile=cpu up
   ```
   - This pulls and runs containers needed for the AI starter kit: AMA, Postgres, and Quadrant.
   - Check Docker Desktop for running containers named **AMA, Postgres,** and **Quadrant**.

### Step 3: Access the Local Workflow Dashboard

1. Open a web browser and navigate to `http://localhost:5678`.
2. Sign in or create an account if it’s your first time accessing it.

### Step 4: Set Up Chat Trigger

1. In the workflow editor, add a "Chat Trigger" node:
   - Enable **file uploads** so users can add their own documents.
   - This feature allows users to interact directly with uploaded files.

### Step 5: Add the Vector Database

1. Add a "Vector Database" node to the workflow.
2. Select the **Quadrant Vector Store** (installed via Docker).
3. Choose the **Insert** operation mode and add a collection by using a unique session ID to store documents.

### Step 6: Set Up Embeddings and Document Loader

Embeddings are crucial to storing uploaded documents in the vector store.

1. Add an **Embedding Node**:
   - Use AMA’s embedding model, which is preloaded with credentials thanks to Docker.
   - To load embedding models, use commands such as:
     ```bash
     ama pull snowflake_arctic
     ```
2. Use Docker Desktop to load models:
   - Click "Exec" in the AMA container.
   - Enter commands to pull desired embedding models.

### Step 7: Connect Components

Now it's time to integrate embeddings, vector storage, and the chat model.

1. **Embedding Loader**: Set data type to **binary** and use a **token splitter** (chunk size = 550).
2. **Chat Model**: Add the **AMA chat model** (e.g., `Gemma 2B`). Set temperature parameters to control response accuracy.
3. **Vector Store Tool**: Add a **Vector Store** tool to retrieve information from Quadrant. Connect this to the vector storage setup earlier.

### Step 8: Testing and Running the Setup

With everything in place, you can test the AI agent:

1. **Run the Agent**:
   - Upload a document (e.g., Bitcoin Whitepaper).
   - Ask questions such as "What is the Genesis block?"
2. **Monitor Docker Logs**: Watch Docker Desktop for container activity, and access the Quadrant Vector Store Dashboard at `http://localhost:6333/dashboard`.

### Step 9: Add AI Agent and Execute Retrieval

Add an AI agent to handle responses using the uploaded documents:

1. **Add a Conversational Agent**: Use a conversational agent instead of a tool-based agent. Set the chat prompt to use inputs from the chat message received node.
2. **Memory (Optional)**: You can enable PostgreSQL for storing conversation history.
3. **Vector Store Retrieval**: Retrieve information from Quadrant, mapping session IDs to access the right document.
4. **Test the AI Agent**: Delete previous chat inputs and try adding new files and questions to verify proper response handling.

---

## Notes and Best Practices

- **Docker Command Line vs. GUI**: Use Docker CLI or the Docker Desktop GUI to pull models—the GUI may be more user-friendly for beginners.
- **Avoiding Hallucinations**: Set lower sampling temperatures for factual outputs to ensure response accuracy.
- **Vector Dimensions**: Different models have different vector dimensions. If switching models, update vector database settings accordingly to avoid dimension mismatch errors.
- **Persistent Memory**: Enable PostgreSQL in the workflow to retain context for richer responses.

---

## Error Handling

- **Dimension Mismatch**: This error indicates different vector dimensions between embedding models. To solve this, delete the current collection in the Vector Store and recreate it with the correct dimensions.
- **404 Error for Public Chats**: When making a chat publicly available, ensure the session is active to prevent this error.

## Final Thoughts

By following this guide, you can set up a self-hosted AI system that runs locally, leveraging open-source models and databases. You can further customize the system to meet your needs, such as embedding the chat on a website or creating AI-driven personal assistants. This is cost-effective, private, and can be a powerful tool for your projects.

Feel free to adapt these steps to your unique requirements. Experiment with different embeddings, chat models, or even swap out components to explore further. Have fun building!

Happy experimenting!

[[Ollama]]   [[N8N Masterclass]] [[LLM]]  [[AI Agents]]