---
github_link: https://github.com/superlinear-ai/raglite
tags:
- rag
- python
video-url: https://www.youtube.com/watch?v=mEmUN4lgpaU&list=WL&index=1
---

## **RAGLite - Python Toolkit for RAG

**Overview of Fahad Mza's Tutorial on Implementing RAG with RAG Light**

In the tutorial, Fahad introduces **Retrieval Augmented Generation (RAG)**, a technique used to provide Large Language Models (LLMs) with factual context about personalized data. Specifically, he explains the **RAG Light** toolkit, a Python-based solution that allows users to implement RAG locally and privately using **SQLite** or **PostgreSQL** for data storage. The RAG Light tool is described as simple, lightweight, and practical for deploying local AI applications without cloud dependencies. The tutorial includes step-by-step installation of all the necessary components, including **LLMs** and **embedding models**, alongside demonstrations on how to run a RAG workflow.

### Why Use RAG Instead of Fine-Tuning

Fahad explains that when you want an LLM like **Llama** to understand personalized information, there are two options:

1. **Fine-tuning the Model**: Training the LLM on personalized data is time-consuming, costly, and sometimes impractical for changing use cases.
2. **Retrieval Augmented Generation (RAG)**: Instead of training, we can use RAG to store personalized data in a **Vector Store** and dynamically retrieve relevant information during inference. This process involves converting documents into **embeddings** (numerical representations) and storing them in a database to allow the LLM to query this information contextually.

### RAG Workflow

1. **Document Chunking**: Divide the document (e.g., a PDF) into smaller parts or **chunks**.
2. **Convert to Embeddings**: Transform these chunks into numerical representations called embeddings using **embedding models**.
3. **Store Embeddings**: Save these embeddings in a vector store, which can be **SQLite** or **PostgreSQL**.
4. **Perform Similarity Search**: When a user asks a question, convert the prompt into embeddings and perform a **similarity search** in the vector store to find relevant information.
5. **Contextual Answer Generation**: Append the retrieved information to the LLM prompt, enabling it to generate a contextually relevant answer.

### RAG Light Toolkit Setup Instructions

**RAG Light** is a Python toolkit designed to facilitate this RAG workflow. Fahad shows how to set up RAG Light along with other components, using **Llama CPP Python** for LLM inference and **SQLite** as the vector store.

#### Step-by-Step Setup

1. **Create a Virtual Environment**
   - Use Python 3.10, as the software is version-sensitive.
   ```bash
   python3.10 -m venv myenv
   source myenv/bin/activate  # For Linux/Mac
   myenv\Scripts\activate   # For Windows
   ```

2. **Install Hugging Face Hub**
   - Log in to Hugging Face to download the models.
   ```bash
   pip install huggingface_hub
   huggingface-cli login  # Requires access token from Hugging Face website
   ```

3. **Install NLP Model for Embedding**
   - Install **sentence-transformers** for NLP-related tasks.
   ```bash
   pip install spacy
   pip install sentence-transformers
   ```

4. **Install Llama CPP Python**
   - Install **Llama CPP Python**, which is a binding for the **Llama CPP** C++ implementation of Llama.
   - Example command for installing the specific version:
   ```bash
   pip install llama-cpp-python==0.2.0  # Version-sensitive
   ```
   - Ensure CUDA is correctly installed for GPU usage. Check using:
   ```bash
   nvidia-smi
   ```

5. **Install RAG Light**
   - Install the RAG Light toolkit along with **Streamlit** if needed.
   ```bash
   pip install rag-light
   pip install streamlit  # Optional, not always stable
   ```

6. **Install SQLite**
   - Install **SQLite** to use as the local database.
   ```bash
   sudo apt-get install sqlite3  # For Linux
   pip install pysqlite3  # Alternatively
   ```
   - Create a database for storing embeddings:
   ```sql
   sqlite3 rag_light.db
   .exit
   ```

7. **Configure RAG Light**
   - Import and configure **RAG Light** in Python.
   ```python
   from rag_light import RAGLightConfig

   config = RAGLightConfig(
       database_path='rag_light.db',
       llm_model_path='models/llama3_18b',
       embedding_model_path='models/embedding_model'
   )
   ```

8. **Run RAG Workflow**
   - Load your personalized document, chunk it, convert it into embeddings, and store in SQLite.
   ```python
   from rag_light import DocumentProcessor

   processor = DocumentProcessor(config)
   processor.insert_document('path/to/your/document.pdf')  # Load and insert chunks into database
   ```
   - Run a query using RAG:
   ```python
   from rag_light import RAG

   rag = RAG(config)
   prompt = "Who is Fahad Mza?"
   response = rag.generate(prompt)
   print(response)
   ```

### Using RAG Light with PostgreSQL

Fahad recommends using **PostgreSQL** for production environments because of its superior scalability and features compared to SQLite. To use PostgreSQL:

- Install PostgreSQL:
  ```bash
  sudo apt-get install postgresql
  ```
- Replace **SQLite** with **PostgreSQL** in the configuration.

```python
config = RAGLightConfig(
    database_path='postgresql://username:password@localhost:5432/rag_light',
    llm_model_path='models/llama3_18b',
    embedding_model_path='models/embedding_model'
)
```

### Summary

Fahad's tutorial showcases how to build a simple, lightweight, and private RAG implementation using **RAG Light**. The process involves setting up an environment with Llama CPP Python, SQLite or PostgreSQL, and integrating Hugging Face models for embeddings. The tutorial is ideal for those looking to experiment with RAG locally and privately without depending on costly cloud services.

### Suggested Next Steps

1. **Experiment Locally**: Start with SQLite to understand how RAG works before moving on to more complex databases like PostgreSQL.
2. **Use Your Own Data**: Try using personal documents as input to see how the RAG workflow processes them and answers questions contextually.
3. **Expand to Production**: Consider shifting to PostgreSQL and improving hardware resources if you're aiming to use RAG Light in a production environment.

[[RAG]]  [[Python]]