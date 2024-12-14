---
tags:
- llamaindex
- ollama
- rag
- chromadb
video-url: https://www.youtube.com/watch?v=NjkAMVFv8m8&list=WL&index=3
---
# Detailed Overview of RAG Using Ollama, LLamaIndex, Chroma DB, LangChain

### Overview

Retrieval-Augmented Generation (RAG) improves the response quality of language models by providing context from a private dataset. This implementation uses the following components:

1. **Ollama**: Open-source tool to run large language models locally.
2. **LlamaIndex**: Helps index documents and store data in vector databases.
3. **Chroma DB**: Open-source vector database for storing document embeddings.
4. **LangChain**: Framework to connect and manage components for building LLM-based applications.

The goal is to create a system where data stored in Chroma DB is retrieved and used to augment a prompt given to a language model, enhancing the generated responses.

### Steps to Implement the End-to-End RAG System

#### Install Required Libraries

```bash
pip install llama-index langchain chromadb openai
```

#### Import Required Modules

```python
import openai
import ollama
from langchain.chains import RetrievalQA
from langchain.vectorstores import Chroma
from langchain.llms import OpenAI, Ollama
from langchain.prompts import PromptTemplate
from langchain.retrievers import ChromaRetriever
```

#### 1. Initialize Chroma Vector Database

Create a Chroma DB instance to store document embeddings.

```python
from langchain.vectorstores import Chroma
from llama_index import SimpleDirectoryReader, VectorStoreIndex

# Initialize Chroma DB
chroma_db = Chroma()

# Create an index of your documents and store them in Chroma
documents = SimpleDirectoryReader('/path/to/your/documents').load_data()
vector_store_index = VectorStoreIndex.from_documents(documents, vector_store=chroma_db)
```

Replace `/path/to/your/documents` with the local path to your documents.

#### 2. Initialize LangChain Retriever

Use a retriever to pull out relevant documents from Chroma DB.

```python
# Create a retriever to query the Chroma DB
retriever = ChromaRetriever(vector_store=chroma_db)
```

#### 3. Initialize the Language Model

Use OpenAI or Ollama as the language model:

```python
# Initialize Ollama LLM model (run locally)
llm_ollama = Ollama(model_name='your_model_name_here')  # Replace with your Ollama model name

# Initialize OpenAI model (requires an API key)
openai.api_key = 'your_openai_api_key_here'
llm_openai = OpenAI(model_name='gpt-3.5-turbo')
```

Replace `your_openai_api_key_here` with your OpenAI API key, and `your_model_name_here` with the appropriate Ollama model name.

#### 4. Create a Prompt Template

Define a prompt template that includes a context retrieved from Chroma DB and the user’s question.

```python
from langchain.prompts import PromptTemplate

prompt_template = PromptTemplate(
    input_variables=['context', 'question'],
    template="Answer the question using the given context.\n\nContext: {context}\n\nQuestion: {question}\n"
)
```

#### 5. Construct the Retrieval-Augmented Generation Chain

Use LangChain to connect the retriever, prompt, and language model.

```python
from langchain.chains import LLMChain

# Create an LLM chain that takes the retriever, prompt template, and LLM model
rag_chain = LLMChain(
    retriever=retriever,
    prompt_template=prompt_template,
    llm=llm_ollama  # Replace with llm_openai for using OpenAI
)
```

#### 6. Ask Questions

Ask questions to see the combined result of context retrieval and model generation.

```python
# Use the chain to ask a question
response = rag_chain.run({
    "question": "How many children does Naresh have?"
})

print(response)
```

### Workflow Summary

1. **Data Preparation**: Index data into a vector database (Chroma) using LlamaIndex.
2. **Retriever Creation**: Use the retriever to search for context in Chroma DB.
3. **RAG Chain**: Construct the RAG chain that pulls context, constructs a prompt, and generates an answer.
4. **Ask Questions**: Interact with the model to obtain answers augmented by relevant document data.

### Example Use Cases

- **Question Answering**: The RAG system can answer specific questions based on indexed data.
- **Personal Information Management**: Embed personal documents (like PDFs) to enable precise answers about personal information.

### Troubleshooting

- **Slow Responses with Ollama**: Running large models locally can be slow if hardware is limited. Optimize hardware resources or offload processing to the cloud.
- **Errors During Retrieval**: Ensure Chroma DB is properly initialized and all documents are correctly embedded.

### Code for Switching Between OpenAI and Ollama

Dynamically switch between OpenAI and Ollama:

```python
def get_llm(model_type="ollama"):
    if model_type == "openai":
        return llm_openai
    else:
        return llm_ollama

selected_llm = get_llm("openai")  # Replace "openai" with "ollama" to use Ollama locally

rag_chain = LLMChain(
    retriever=retriever,
    prompt_template=prompt_template,
    llm=selected_llm
)

# Ask question
response = rag_chain.run({"question": "What are the certifications Naresh has?"})
print(response)
```

[[Ollama]]  [[RAG]]  [[ChromaDB]]  [[LlamaIndex Framework]]  [[Python]]  

