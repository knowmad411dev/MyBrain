---
tags:
- ollama
- python
- agents
video-url: https://www.youtube.com/watch?v=5xPvsMX2q2M&list=WL&index=3
---

## **Overview of Ollama Memory AI Agent**

The **Ollama Memory AI Agent** is a local AI system designed to provide users with conversational memory while ensuring **100% data privacy and security**. Unlike cloud-based solutions, all data is stored locally, allowing for complete ownership of user interactions. This agent utilizes **Retrieval-Augmented Generation (RAG)** to efficiently fetch and use context during conversations, giving highly accurate responses.

#### **Features**

- **Local Data Storage**: Stores all conversations locally in a vector database, ensuring data privacy.
- **Embeddings for Context Retrieval**: Uses advanced machine learning embeddings to extract meaning from conversations, enabling contextually rich interactions.
- **Multiple Language Models**: Supports Ollama open-source models, which are quantized for efficient local performance, even on consumer PCs.
- **Slash Commands for User Control**:
  - `/recall`: Retrieve context from the vector database to enhance the response.
  - `/forget`: Forget the last conversation from memory.
  - `/memorize`: Save the prompt without generating a response.

#### **Requirements**

1. **Python**: Version 3.11 or 3.12.
2. **Ollama API**: Installed locally for language model inference.
3. **Libraries**: Install using `requirements.txt`.
    - `chromadb`: Vector database for embedding storage.
    - `psycopg2`: PostgreSQL driver for Python.
    - `tqdm`: Progress bar for user experience.
    - `colorama`: For colored terminal output.

#### **Setup Instructions**

1. **Install Python**: Ensure Python 3.11 or 3.12 is correctly installed.
   ```bash
   python -m pip install --upgrade pip
   ```
2. **Set Up Ollama**: Download and set up the Ollama API.
3. **Prepare the Project**:
   - Create a new directory to store the program files.
   - Open the folder in VSCode.
   - Create a `requirements.txt` file:
     ```plaintext
     chromadb

tqdm

     colorama

     psycopg2

     ```

   - Install dependencies:
     ```bash
     pip install -r requirements.txt
     ```
4. **Configure PostgreSQL**: Create a user, database, and table.
   ```sql
   CREATE USER myuser WITH PASSWORD 'mypassword' SUPERUSER;
   CREATE DATABASE memory_agent;
   \c memory_agent
   CREATE TABLE conversations (
       id SERIAL PRIMARY KEY,
       timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
       prompt TEXT NOT NULL,
       response TEXT NOT NULL
   );
   ```

#### **Core Code Implementation**

Here is the core structure of the Python code broken into modular steps:

##### **1. Initialize Dependencies**

```python
import chromadb
import psycopg2
from tqdm import tqdm
from colorama import Fore, Style
import ollama

# Database connection parameters
DB_PARAMS = {
    "dbname": "memory_agent",
    "user": "myuser",
    "password": "mypassword",
    "host": "localhost",
    "port": 5432,
}
```

##### **2. PostgreSQL Integration**

```python
def connect_db():
    con = psycopg2.connect(**DB_PARAMS)
    return con

def fetch_conversations():
    con = connect_db()
    with con.cursor() as cursor:
        cursor.execute("SELECT * FROM conversations;")
        conversations = cursor.fetchall()
    con.close()
    return conversations

def store_conversation(prompt, response):
    con = connect_db()
    with con.cursor() as cursor:
        cursor.execute(
            "INSERT INTO conversations (prompt, response) VALUES (%s, %s);",
            (prompt, response)
        )
        con.commit()
    con.close()
```

##### **3. Vector Embedding with ChromaDB**

```python
client = chromadb.Client()

def create_vector_db(conversations):
    vector_db = client.create_collection("conversations")
    for convo in conversations:
        serialized_convo = f"Prompt: {convo['prompt']} | Response: {convo['response']}"
        embedding = ollama.embedding("nomic/embed-text", prompt=serialized_convo)["embedding"]
        vector_db.add(ids=[str(convo['id'])], embeddings=[embedding], documents=[serialized_convo])
    return vector_db
```

##### **4. Retrieve Embeddings**

```python
def retrieve_embeddings(prompt, vector_db, results_per_query=2):
    prompt_embedding = ollama.embedding("nomic/embed-text", prompt=prompt)["embedding"]
    results = vector_db.query(query_embeddings=[prompt_embedding], n_results=results_per_query)
    return results["documents"]
```

##### **5. LLM Chat and Commands**

```python
def chat_with_model(convo, prompt):
    response = ollama.chat(model="llama-2", messages=convo)
    return response["content"]

def recall_context(prompt, vector_db):
    embeddings = retrieve_embeddings(prompt, vector_db)
    context = " ".join(embeddings)
    return context
```

##### **6. User Commands**

```python
def handle_commands(prompt, convo, vector_db):
    if prompt.startswith("/recall"):
        context = recall_context(prompt[8:], vector_db)
        print(Fore.YELLOW + "Recalling context..." + Style.RESET_ALL)
        convo.append({"role": "system", "content": context})
    elif prompt.startswith("/forget"):
        # Logic for forgetting
        print(Fore.RED + "Forgetting last conversation..." + Style.RESET_ALL)
    elif prompt.startswith("/memorize"):
        # Logic for memorizing
        print(Fore.GREEN + "Memorizing prompt..." + Style.RESET_ALL)
    else:
        response = chat_with_model(convo, prompt)
        store_conversation(prompt, response)
        print(Fore.LIGHTGREEN_EX + response + Style.RESET_ALL)
        convo.append({"role": "assistant", "content": response})
```

#### **Final Notes**

- **Run Ollama API**: Ensure the API is up and running before starting the script.
- **Experimentation**: Test different language models and hyperparameters to optimize performance based on your hardware.
- **Enhancements**: Multi-query context retrieval and additional context classification can further enhance performance.

---

[[Ollama]]  [[Python]]  [[ChromaDB]]
