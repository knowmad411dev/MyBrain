---
Video-URL: https://www.youtube.com/watch?v=FQTCLOUnIzI
tags:
- rag
- chromadb
---

# Building a Simple Retrieval Augmented Generation (RAG) System

In this guide, we'll walk through the steps to build a simple Retrieval Augmented Generation (RAG) system using Python and TypeScript. Additionally, we'll explore tools that allow you to implement RAG without any coding.

## Table of Contents

1. [Overview](#overview)
2. [Tasks to Accomplish](#tasks-to-accomplish)
3. [Task 1: Setup the Environment](#task-1-setup-the-environment)
    - [Choosing a Vector Store](#choosing-a-vector-store)
    - [Using Chroma with Docker](#using-chroma-with-docker)
4. [Task 2: Bring Text into the Database](#task-2-bring-text-into-the-database)
    - [Python Implementation](#python-implementation)
    - [Running the Python Script](#running-the-python-script)
    - [Verifying Data in Chroma](#verifying-data-in-chroma)
5. [Task 3: Implementing in TypeScript](#task-3-implementing-in-typescript)
    - [Using Deno with TypeScript](#using-deno-with-typescript)
    - [Running the TypeScript Script](#running-the-typescript-script)
6. [Task 4: Query the Database](#task-4-query-the-database)
    - [TypeScript Example](#typescript-example)
    - [Python Example](#python-example)
7. [Conclusion](#conclusion)
8. [Additional Resources](#additional-resources)

---

## Overview

Retrieval Augmented Generation (RAG) combines retrieval-based methods with generative models to produce more accurate and contextually relevant responses. This guide covers setting up the environment, importing data, and querying the database using both Python and TypeScript.

## Tasks to Accomplish

1. **Setup the Environment**
2. **Bring Text into the Database**
3. **Implement the System in Python and TypeScript**
4. **Query the Database**

## Task 1: Setup the Environment

### Choosing a Vector Store

The vector store is a critical component of the RAG system, responsible for storing and retrieving document embeddings. You have two primary options:

- **Hosted Vector Stores:**
  - **Supabase**: A popular choice with robust features.
  - **Others**: Numerous other hosted solutions are available.
- **Self-Hosted Vector Stores:**
  - **Chroma**: Highly recommended for its ease of use and functionality.
  - **Others**: Multiple self-hosted options exist based on your requirements.

### Using Chroma with Docker

Chroma is an excellent choice for a self-hosted vector store. Running Chroma via Docker is straightforward and ensures data persistence.

#### Docker Command

```bash
docker run -d -p 8000:8000 -v chroma-data:/chromadb/data chromadb/chroma
```

- **Flags:**
  - `-d`: Run the container in detached mode.
  - `-p 8000:8000`: Map port 8000 of the container to port 8000 on the host.
  - `-v chroma-data:/chromadb/data`: Mount the volume `chroma-data` to persist data.

After running this command, Chroma will be accessible at `http://localhost:8000`.

## Task 2: Bring Text into the Database

### Python Implementation

We'll use Python to import text documents into the Chroma database. The process involves reading files, chunking the text, generating embeddings, and storing them in the database.

#### Steps:

1. **Create a Collection:**
   - Initialize a Chroma client and create a collection to store documents.

2. **Read and Chunk Text Files:**
   - Read the contents of text files from a specified directory.
   - Split the text into manageable chunks (e.g., 100 words per chunk).

3. **Generate Embeddings:**
   - Use Ollama's embedding API to generate embeddings for each text chunk.

4. **Add Documents to Chroma:**
   - Each document should include:
     - **ID**: Unique identifier.
     - **Document**: The text chunk.
     - **Embedding**: The generated embedding.
     - **Metadata**: Additional information (e.g., source filename).

#### Example Code (`importdocs.py`)

```python
import os
import chromadb
from chromadb.config import Settings
from ollama import Ollama

# Initialize Chroma client
client = chromadb.Client(Settings(
    chroma_api_impl="rest",
    chroma_server_host="localhost",
    chroma_server_http_port="8000"
))
collection = client.create_collection("my_collection")

# Function to read files
def read_files(path):
    files = {}
    for filename in os.listdir(path):
        if filename.endswith(".txt"):
            with open(os.path.join(path, filename), 'r', encoding='utf-8') as file:
                files[filename] = file.read()
    return files

# Function to chunk text
def chunk_text(text, chunk_size=100):
    words = text.split()
    return [' '.join(words[i:i + chunk_size]) for i in range(0, len(words), chunk_size)]

# Function to generate embeddings
def generate_embeddings(chunks):
    ollama = Ollama()
    return ollama.embed(chunks)

# Import documents
files = read_files("path/to/scripts")
for filename, text in files.items():
    chunks = chunk_text(text)
    embeddings = generate_embeddings(chunks)
    documents = [{
        "id": f"{filename}-{i}",
        "document": chunk,
        "embedding": embedding,
        "metadata": {"source": filename}
    } for i, (chunk, embedding) in enumerate(zip(chunks, embeddings))]
    collection.add(documents=documents)
```

### Running the Python Script

Execute the following command to import documents:

```bash
python importdocs.py
```

### Verifying Data in Chroma

1. **Access Chroma's Documentation Endpoint:**

   Navigate to `http://localhost:8000/docs` in your browser.

2. **Get Collections:**

   - Find the `/api/v1/collections` GET endpoint.
   - Click **Try it Out** and then **Execute**.
   - You should see a response with information about your collections.

3. **Retrieve Documents from a Collection:**

   - Copy the `collection_id` from the previous response.
   - Scroll to the `/api/v1/collections/{collection_id}/get` POST endpoint.
   - Click **Try it Out**.
   - Paste the `collection_id` and remove everything above `limit` in the request body.
   - Execute to see all documents in the collection.

## Task 3: Implementing in TypeScript

We'll replicate the Python implementation using TypeScript and Deno.

### Using Deno with TypeScript

Deno is a modern runtime for JavaScript and TypeScript. It provides a secure and efficient environment for running TypeScript code.

#### Example Code (`importdocs.ts`)

```typescript
import { ChromaClient } from 'https://deno.land/x/chroma_client/mod.ts';
import { readFiles, chunkText, generateEmbeddings } from './utils.ts';

// Initialize Chroma client
const client = new ChromaClient({ host: 'localhost', port: 8000 });
const collection = await client.createCollection('my_collection');

// Import documents
const files = await readFiles('path/to/scripts');
for (const [filename, text] of Object.entries(files)) {
    const chunks = chunkText(text, 100);
    const embeddings = await generateEmbeddings(chunks);
    const documents = chunks.map((chunk, i) => ({
        id: `${filename}-${i}`,
        document: chunk,
        embedding: embeddings[i],
        metadata: { source: filename }
    }));
    await collection.addDocuments(documents);
}
```

**Note:** Ensure you have a `utils.ts` file that contains the `readFiles`, `chunkText`, and `generateEmbeddings` functions similar to the Python implementation.

### Running the TypeScript Script

Execute the following command to import documents using Deno:

```bash
deno task import
```

*Note: Ensure you have a `deno.json` configuration file with the appropriate task defined.*

## Task 4: Query the Database

### TypeScript Example

We'll create a script to query the Chroma database and generate responses using RAG.

#### Example Code (`search.ts`)

```typescript
import { ChromaClient } from 'https://deno.land/x/chroma_client/mod.ts';
import { Ollama } from 'https://deno.land/x/ollama/mod.ts';

// Initialize Chroma client
const client = new ChromaClient({ host: 'localhost', port: 8000 });
const collection = await client.getCollection('my_collection');

// Get question from command line
const question = Deno.args[0];
if (!question) {
    console.error("Please provide a question.");
    Deno.exit(1);
}

// Generate embedding
const ollama = new Ollama();
const embedding = (await ollama.embed([question]))[0];

// Query the database
const results = await collection.query({
    embedding,
    top_k: 5
});

// Build prompt
const context = results.documents.map(doc => doc.document).join('\n');
const prompt = `Answer the following question based on the provided context:\n\n${context}\n\nQuestion: ${question}`;

// Generate answer
const answer = await ollama.generate(prompt);
console.log('With RAG:', answer);
```

#### Running the TypeScript Query

Execute the following command to perform a search:

```bash
deno task search "what is ollama"
```

### Python Example

Similarly, you can perform a query using Python.

#### Example Code (`search.py`)

```python
import sys
import chromadb
from chromadb.config import Settings
from ollama import Ollama

# Initialize Chroma client
client = chromadb.Client(Settings(
    chroma_api_impl="rest",
    chroma_server_host="localhost",
    chroma_server_http_port="8000"
))
collection = client.get_collection("my_collection")

# Get query from command line
if len(sys.argv) < 2:
    print("Please provide a question.")
    sys.exit(1)

question = sys.argv[1]

# Generate embedding
ollama = Ollama()
embedding = ollama.embed([question])[0]

# Query the database
results = collection.query(
    embedding=embedding,
    n_results=5
)

# Build prompt
context = "\n".join([doc['document'] for doc in results['documents']])
prompt = f"Answer the following question based on the provided context:\n\n{context}\n\nQuestion: {question}"

# Generate answer
answer = ollama.generate(prompt)
print("With RAG:", answer)
```

#### Running the Python Query

Execute the following command to perform a search:

```bash
python search.py "what is ollama"
```

## Conclusion

Building a RAG system involves setting up a vector store, importing and managing documents, and implementing querying mechanisms. Whether you choose Python or TypeScript, the process is straightforward with the right tools. Additionally, pre-built tools like Open WebUI, MSTY, Page Assist, and AnythingLLM offer RAG functionalities without the need for extensive coding.

## Additional Resources

- **GitHub Repository:** [videoprojects](https://github.com/technovangelist/videoprojects) (Contains the project code in the `2024-09-10-buildrag` directory)
- **Chroma Documentation:** [Chroma Docs](https://www.trychroma.com/docs)
- **Ollama API:** [Ollama API Documentation](https://ollama.com/docs/api)
- **Deno:** [Deno Official Website](https://deno.land/)
- **Pre-built RAG Tools:** Explore tools like [Open WebUI](https://github.com/OpenWebUI), [MSTY](https://github.com/MSTY), [Page Assist](https://pageassist.com), and [AnythingLLM](https://anythingllm.com)

---

[[ChromaDB]] [[RAG]] [[Python]]