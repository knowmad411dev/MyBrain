---
tags:
- ollama
- chromadb
- python
- rag
video-url: https://www.youtube.com/watch?v=g8fMRuGR5z0&list=WL&index=2
---
## **Overview of Retrieval-Augmented Generation (RAG)**

### **Introduction to RAG**

Retrieval-Augmented Generation (RAG) is a technique in AI models that involves feeding relevant information retrieved at runtime to the model. This helps improve the model's response quality by avoiding hallucinations and enhancing its context awareness with precise and up-to-date information. This technique is particularly effective when an AI model needs to provide factual responses based on data that may change frequently, such as sales forecasts.

**Example:**
- Suppose a user asks, "Was this week's sales higher than last week?" The model would perform poorly if it tried to generate an answer without real-time context. Instead, RAG retrieves the necessary sales forecast and feeds it to the model at runtime, ensuring a more accurate response.

### **Techniques for Implementing RAG**

1. **Simple Prompting:**
   - A straightforward way to implement RAG is by adding the relevant information directly into the prompt.
   - Example: Add basic information like "Today is Sunday, September 2nd, and the user's name is Sanj Jam" to the prompt.
   - This approach works well for narrow use cases where the model needs specific information, such as recent sales forecasts or weather data.
   - **Limitations:** This method is not flexible for handling larger data or dynamic requests and is limited by the model’s context window.

2. **Vector Databases and Cosine Similarity:**
   - The more scalable approach to RAG involves using a **Vector Database (Vector DB)** and **cosine similarity**.
   - **Steps involved:**
     1. Store relevant documents (e.g., sales forecasts) in a Vector DB.
     2. When the user asks a question, the relevant documents are retrieved using cosine similarity based on the query content.
     3. These documents are then added to the model’s context.
   - **Example:** When asked, "How do our sales this week compare to the same time last year?", the model can retrieve documents related to the same timeframe (e.g., December 15th of the previous year) from the Vector DB and use it for comparison.

3. **Specialized AI Agents:**
   - Another level above RAG involves using **specialized AI agents** that work together, where each agent is specialized in a specific domain.
   - **Example:** In a car dealership scenario, a user might ask about a service schedule at a particular location. An AI agent specific to the **northeastern location** handles the query, making the system more efficient and specialized.

4. **Massive Context Windows (Advanced RAG by Google):**
   - The most advanced form involves using AI models with massive context windows to handle vast amounts of data without needing specialized retrieval systems.
   - **Example:** Google’s Gemini model, which can handle up to **1 million tokens** in a context window, allows entire textbooks to be processed without relying on RAG.
   - **Limitation:** This approach is feasible only for companies with massive computing power, such as Google and Meta.

### **Implementation Example: Building RAG with Python**

The example focuses on building a simple RAG system using **Vector DB and cosine similarity**. The implementation is done in Python using libraries such as **ChromaDB**, **PyPDF2**, and others. The dataset consists of two technical papers: "Meta Chameleon" and "Gemma 2".

---

## **Detailed Walkthrough of the Example**

### **1. Setting Up the Environment**

To implement a RAG-based system, we need to set up a Python environment and install the necessary libraries.

**How-to Instructions:**
- Create a virtual environment:
  ```bash
  python -m venv rag_tutorial_env
  ```
- Activate the virtual environment and install the following dependencies:
  - **Ollama**: Access the language model.
  - **ChromaDB**: A vector database for document storage and retrieval.
  - **PyPDF2**: To extract text from PDF files.

  ```bash
  pip install ollama chromadb pypdf2
  ```

### **2. Writing the Code (Main Script - main.py)**

The main part of the code involves setting up a vector database and using cosine similarity for information retrieval.

#### **Step 1: Import Libraries and Initialize ChromaDB Client**

- Import the necessary libraries:
  ```python
  import chromadb

  # Set up the ChromaDB client
  chroma_client = chromadb.Client()
  collection = chroma_client.get_or_create_collection(name="rag_tutorial")
  ```

#### **Step 2: Uploading PDF Files to ChromaDB**

- A function to upload PDF files to ChromaDB:
  ```python
  from PyPDF2 import PdfReader

  def upload_pdf(file_path):
      # Open and read the PDF
      with open(file_path, 'rb') as f:
          pdf = PdfReader(f)
          document_id = 0

          for page in pdf.pages:
              # Add each page to the ChromaDB collection
              text = page.extract_text()
              collection.add(documents=[text], ids=[f"{file_path}_{document_id}"])
              document_id += 1

  # Uploading two technical papers
  upload_pdf('chameleon_tech_paper.pdf')
  upload_pdf('gemma2_tech_paper.pdf')
  ```

- **Explanation**: Each page of the document is treated as a separate entity in the database to enable fine-grained retrieval later on.

#### **Step 3: Handling User Queries**

- Get a query from the user and retrieve relevant documents from ChromaDB.
  ```python
  user_query = input("Enter your query: ")

  # Query the collection to get the closest pages
  closest_pages = collection.query(query_texts=[user_query], n_results=3)

  # Pass these pages to the language model
  context_documents = [page['document'] for page in closest_pages]
  ```

#### **Step 4: Integrating with the LLM**

- To get a response, we use a language model (e.g., **Llama 3.1**).
  - We provide the model with the context obtained from ChromaDB, along with the user query.
  ```python
  from ollama import LLM

  model = LLM.load("llama3.1")
  response = model.chat(context=context_documents, query=user_query)
  print(response)
  ```

---

## **Key Learnings and Concepts**

### **1. Vector DB and Cosine Similarity**

- **Vector DB** is used to store document embeddings.
- **Cosine Similarity** is used to determine how similar the stored document vectors are to the user query, ensuring that the closest relevant information is retrieved.

### **2. Context Window Limitations**

- Models have limited **context windows** that restrict the amount of data you can feed to them at runtime.
- Using RAG allows us to overcome this limitation by dynamically selecting the most relevant information.

### **3. Specialized Agents vs. General Models**

- Having specialized AI agents can help achieve more efficient, domain-specific performance.
- This modular approach allows systems to scale more efficiently and be more responsive to specific types of queries.

### **4. Trade-offs in RAG Systems**

- Using **smaller models** like Llama 3.1 with retrieval is cost-effective since the retrieval step ensures that the model always has the most relevant information.
- **Massive models** like Google’s Gemini can handle huge amounts of context, but they are costly and limited to organizations with immense resources.

---

## **Practical Tips and Next Steps**

1. **Multi-Turn Conversations:**
   - Modify the code to handle multi-turn conversations, allowing the AI to remember previous queries and build on them.
   - Incorporate more sophisticated retrieval mechanisms, such as chunking large documents into smaller, more manageable parts.

2. **Use Cases for RAG:**
   - Business applications like sales analysis or customer support chatbots.
   - Specialized systems that handle different locations, datasets, or operational domains.

3. **Experimentation:**
   - Add more diverse document types like Wikipedia pages, HTML articles, and corporate documents.
   - Experiment with different language models, including smaller models that could provide cost savings if fed with high-quality retrieved information.

4. **Specialized Agents:**
   - Expand the system to use **multiple agents**, each handling specific queries. This makes it more scalable and specialized, especially useful in larger organizations.

---

## **Conclusion**

Retrieval-Augmented Generation (RAG) is an important method for enhancing the capabilities of language models by grounding them in factual, up-to-date information. This overview covered both a conceptual and practical understanding of RAG, providing a detailed walkthrough of a simple Python-based RAG system involving Vector DB and cosine similarity.

The code implementation uses **ChromaDB**, **PyPDF2**, and **Ollama** to build a pipeline that efficiently handles document retrieval and LLM interaction, ultimately creating a system that can answer questions accurately using dynamically retrieved data.

By following the guide, you can extend this system to accommodate more complex requirements, such as multi-turn conversations or domain-specific specialized agents, to provide even better performance and accuracy in a wide range of practical applications.

[[Ollama]]  [[ChromaDB]]  [[Python]]  [[RAG]]