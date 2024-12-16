---
Video-URL: https://www.youtube.com/watch?v=3bz0nzs1tRA&list=WL&index=4
tags:
- python
- langchain
- rag
---

## AMA + LangChain.js for RAG

## Overview

In this guide, we explore how to deploy open-source AI models using the AMA platform, offering an alternative to services like Amazon Bedrock and SageMaker. The focus is on setting up and running models locally or in the cloud, leveraging [[Docker]] for deployment, and implementing a memory service using retrieval-augmented generation ([[RAG]]) with an in-memory vector store.

---

## Table of Contents

1. Introduction to AMA
2. Prerequisites
3. Setting Up AMA with Docker
4. Running AI Models on AMA
5. Implementing the Memory Service
6. Configuring the Project
7. Running and Testing the Service
8. Resources and Links

---

## 1. Introduction to AMA

AMA is a platform designed to simplify the deployment and management of open-source AI models. It allows you to run models locally on your machine or deploy them in the cloud, providing a user-friendly interface and robust API support. This makes it easier to implement complex AI functionalities without relying on external services.

### Key Features

- Supports multiple AI models, including Llama for language processing and various embedding models.
- Utilizes Docker for seamless deployment.
- Offers both in-memory and external vector stores for data management.
- Facilitates retrieval-augmented generation (RAG) patterns for enhanced context handling.

---

## 2. Prerequisites

Before diving into the setup, ensure you have the following:

- **Docker Installed**: AMA uses Docker for deployment. Install Docker from [here](https://www.docker.com/get-started).
- **Git Installed**: For cloning repositories. Download [[Git]] from [here](https://git-scm.com/downloads).
- **Basic Knowledge of Python**: Since the project involves Python coding.
- **Familiarity with AI Models**: Understanding of large language models and embeddings will be beneficial.

---

## 3. Setting Up AMA with Docker

### Step 1: Pull the AMA Docker Image

Open your terminal and execute the following command to pull the AMA Docker image:

```bash
docker pull ama/platform:latest
```

### Step 2: Run the AMA Docker Container

Start the AMA container with:

```bash
docker run -d --name ama-container -p 8000:8000 ama/platform:latest
```

- `-d`: Runs the container in detached mode.
- `--name ama-container`: Names the container for easy reference.
- `-p 8000:8000`: Maps port 8000 of the container to port 8000 on your local machine.

### Step 3: Verify the Container is Running

Check if the container is running:

```bash
docker ps
```

You should see `ama-container` listed among the running containers.

---

## 4. Running AI Models on AMA

### Supported Models

AMA supports a variety of models. In this guide, we'll focus on:

- **Llama**: A large language model for generating human-like text.
- **Nomic Embed Text**: An embedding model for converting text into vector representations.

### Step 1: Start the Llama Model

Use the AMA interface or Docker commands to start the Llama model. For example:

```bash
docker exec -it ama-container bash
```

Once inside the container, run:

```bash
start-model llama
```

_Note: The exact command may vary based on AMA's CLI._

### Step 2: Start the Embedding Model

Similarly, start the embedding model:

```bash
start-model nomic-embed-text
```

### Step 3: Test the Models

Interact with the Llama model to ensure it's working:

```python
import requests

response = requests.post("http://localhost:8000/models/llama", 
	json={"prompt": "What is the distance between the Earth and the Moon?"})
print(response.json())
```

_Expected Output: A factual answer regarding the distance between Earth and the Moon._

---

## 5. Implementing the Memory Service

We'll reimplement a memory service that utilizes AMA's models to store and retrieve contextual information.

### Step 1: Clone the Existing Repository

Assuming you have a previous implementation, clone it:

```bash
git clone https://github.com/yourusername/memory-service.git
cd memory-service
```

_Replace_ `_yourusername_` _with your actual GitHub username._

### Step 2: Update Dependencies

Ensure all necessary libraries are installed. Update your `requirements.txt`:

```bash
langchain
llama
nomic-embed-text
ama-client
```

Install the dependencies:

```bash
pip install -r requirements.txt
```

### Step 3: Modify the Memory Service Code

Update the code to integrate AMA's models. Below is a simplified example:

```Python
# memory_service.py
from langchain import RetrievalAugmentedGeneration
from llama import AMAChat
from nomic_embed_text import EmbeddingModel
from vector_store import InMemoryVectorStore

# Initialize AMA Chat with Llama model
llama_chat = AMAChat(model_name="llama", temperature=0.7)

# Initialize Embedding Model
embedding_model = EmbeddingModel(model_name="nomic-embed-text")

# Initialize In-Memory Vector Store
vector_store = InMemoryVectorStore()

# Initialize Retrieval Augmented Generation
rag = RetrievalAugmentedGeneration(
    chat_model=llama_chat,
    embedding_model=embedding_model,
    vector_store=vector_store
)

# Methods to store and retrieve memory
def store_memory(document):
    vector = embedding_model.encode(document)
    vector_store.add(vector, document)

def get_relevant_memory(query):
    vector = embedding_model.encode(query)
    return vector_store.query(vector)
```

---

## 6. Configuring the Project

### Step 1: Update Configuration Files

Remove dependencies related to Amazon Bedrock and OpenSearch, as they are no longer needed.

```python
# Remove or comment out imports related to Bedrock and OpenSearch
# import bedrock
# import opensearch
```

### Step 2: Update Vector Store References

Replace OpenSearch vector store with AMA's in-memory vector store in your code:

```Python
# Previous OpenSearch setup (to be removed)
# from opensearch_vector_store import OpenSearchVectorStore
# vector_store = OpenSearchVectorStore(...)

# New In-Memory Vector Store
from vector_store import InMemoryVectorStore
vector_store = InMemoryVectorStore()
```

### Step 3: Adjust Model References

Ensure that your large language model and embedding model are correctly referenced from AMA:

```Python
llama_chat = AMAChat(model_name="llama", temperature=0.7)
embedding_model = EmbeddingModel(model_name="nomic-embed-text")
```

---

## 7. Running and Testing the Service

### Step 1: Initialize the Memory Service

```Python
# run_service.py
from memory_service import store_memory, get_relevant_memory

def run():
    # Store initial memory
    store_memory("Dora is a German Shepherd who lives with Bob.")

    # Query the memory
    response = get_relevant_memory("Who is Dora?")
    print(response)

if __name__ == "__main__":
    run()
```

### Step 2: Execute the Service

Run the service using Python:

```bash
python run_service.py
```

_Expected Output:_

```
Dora is a German Shepherd dog.
```

### Troubleshooting

- **Import Errors**: If you encounter import errors related to module types, ensure your `package.json` includes the `"type": "module"` line.

    ```JSON
    {
      "name": "memory-service",
      "version": "1.0.0",
      "type": "module",
      ...
    }
    ```

- **Docker Issues**: Ensure the AMA Docker container is running and accessible on the specified port.

---

## 8. Resources and Links

- **AMA Platform Documentation**: [AMA Docs](https://ama-platform.com/docs)
- **GitHub Repository**: [Memory Service Repo](https://github.com/yourusername/memory-service)
- **Docker Installation**: [Get Docker](https://www.docker.com/get-started)
- **LangChain Library**: [LangChain GitHub](https://github.com/langchain/langchain)
- **Llama Model Information**: [Llama Models](https://llama.com)
- **Nomic Embed Text**: [Nomic Embed Text](https://nomic.com)

_Note: Replace placeholder URLs like_ `_https://ama-platform.com/docs_` _and_ `_https://github.com/yourusername/memory-service_` _with actual links relevant to your project._

---

## Conclusion

By following this guide, you've successfully transitioned from using Amazon Bedrock to deploying open-source models via the AMA platform. This setup allows for greater flexibility, reduced dependency on external services, and the ability to run AI models locally or in your preferred cloud environment. The memory service implemented demonstrates how retrieval-augmented generation can be achieved using AMA's supported models and an in-memory vector store.

Feel free to explore further by integrating more models, experimenting with different vector stores, or enhancing the memory service's capabilities. AMA's platform simplifies these processes, making it an excellent choice for developers looking to leverage open-source AI models efficiently.

 [[LangChain]] [[RAG]]  [[Python]]  [[Obsidian with AMA]]