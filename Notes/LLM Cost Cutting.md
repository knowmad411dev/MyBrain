---
Video-URL: https://www.youtube.com/watch?v=kAgSPzlgnDM&list=WL&index=14
tags:
- llm
- langchain
- rag
- python
---

## **LLM Cost Cutting

This video by Eric from LangChain focuses on integrating MongoDB's new semantic caching capabilities to reduce Large Language Model (LLM) costs. MongoDB has released an integration package with LangChain, which enables MongoDB to function as a vector store or cache, including a semantic cache. The video demonstrates two examples: a basic prompt and LLM chain with semantic caching, and a retrieval-augmented generation (RAG) example, covering the benefits and challenges of semantic caching in both contexts.

## Key Concepts

1. **LangChain**: A framework connecting LLMs, vector stores, and tools. It provides abstractions to implement various applications, including academic concepts and basic solutions.
2. **MongoDB Atlas with LangChain**: MongoDB is a NoSQL cloud database with native vector search capabilities. The integration with LangChain allows you to use MongoDB as a vector store for embeddings or as a cache for LLMs.
3. **Other Technologies Used**:

    - **Anthropic’s Claude 3**: Used as an LLM to generate responses.
    - **OpenAI Embeddings**: To create vector representations for semantic caching.
    - **Exa**: A retriever for retrieving documents to form context for RAG tasks.

---

## Setup and Configuration

### Installing Packages

You need to install packages for LangChain and its integrations with MongoDB, Anthropic, OpenAI, and Exa.configuration

```bash
pip install langchain langchain-mongodb langchain-anthropic langchain-openai langchain-exa
```

### Setting Environment Variables

Set environment variables for API keys and configuration parameters. Here's a list of potential variables:

- **MongoDB Connection String**: Contains credentials for connecting to the MongoDB Atlas instance.
- **OpenAI API Key**: For accessing embeddings.
- **Anthropic API Key**: For interacting with their LLM.

### Enabling LangSmith for Debugging

LangSmith is a debugging and observability tool for LangChain applications. To enable LangSmith, you need to set two environment variables, which will allow you to trace the app's flow, see which prompts are used, and track metrics like token usage and costs.

---

## Example 1: Basic Prompting and LLM Chain with Semantic Caching

1. **Creating a Prompt and LLM**:
    - You create a model using Anthropic's Claude 3.
    - Define a prompt template that specifies how to pass context and a question to the LLM.

```python
from langchain_anthropic import ChatAnthropic from langchain_core.prompts import PromptTemplate  model = ChatAnthropic(model_name="claude-v1") 
# Adjust to the desired model  
prompt_template = PromptTemplate.from_template("""     Answer the following question about the given context:     <context>     {context}     </context>     <question>     {question}     </question> """)
```

2. **Invoking the Chain**: You can invoke the LLM by passing the context and question to get a response.

```python
context = "Eric works at LangChain" question = "Where does Eric work?" response = model.invoke({"context": context, "question": question})
```

3. **Implementing Semantic Caching**: Semantic caching stores the results of similar LLM queries to reduce the number of API calls and thus reduce costs.

### Creating a Semantic Cache

- Import and configure the semantic cache using MongoDB Atlas as the backend.

```python
from langchain_mongodb import MongoDBAtlasSemanticCache from langchain_openai import OpenAIEmbeddings import os  connection_string = os.getenv("MONGODB_ATLAS_URI") cache = MongoDBAtlasSemanticCache(     connection_string=connection_string,     collection_name="semantic_cache",     db_name="langchain_db",     index_name="cache_index",     embeddings=OpenAIEmbeddings(model_name="text-embedding-ada-002"),     threshold=0.99 # Cosine similarity threshold )
```

- **Clearing the Cache**: Clear any existing cache entries if needed.

```python
cache.clear()
```

- **Setting the LLM Cache**: Globally set the LLM cache to the configured semantic cache.

```python
from langchain_core.globals import set_llm_cache  set_llm_cache(cache)`
```

4. **Testing Semantic Caching**: Running the same query multiple times will show that the first call makes an API request, while subsequent calls return cached results, significantly reducing response time.

---

## Example 2: RAG (Retrieval-Augmented Generation) Chain with Semantic Caching

1. **Configuring an Exa Retriever**: Use Exa to retrieve documents that form context for the LLM to answer questions.

```python
from langchain_exa import ExaSearchRetriever from langchain_exa.configuration import TextContentOptions  exa_retriever = ExaSearchRetriever(     api_key=os.getenv("EXA_API_KEY"),     text_content_options=TextContentOptions(max_characters=300),     num_documents=3 )
```

2. **Formatting Retrieved Documents**: Join the retrieved documents into a string to serve as context.

```python
def format_docs(docs):     return "\n\n".join(doc.page_content for doc in docs)
```

3. **Building the RAG Chain**: Construct a chain where the input is passed through the Exa retriever to gather context and then to the LLM for generating a response.

```python
from langchain_core.runnables import RunnablePassThrough  question_step = RunnablePassThrough() retriever_step = exa_retriever format_step = format_docs llm_step = model  # Model previously configured
```

4. **Handling Semantic Caching in RAG**: Since semantic caching only caches the LLM's input and output, changes in the context retrieved from the Exa retriever may cause cache misses, even if the questions are semantically similar.

---

## Challenges in Semantic Caching for RAG Applications

- **Semantic vs. Exact Matching**: While semantic caching is robust to minor variations in queries, in a RAG scenario, even semantically similar queries may retrieve different context documents. This leads to cache misses.
- **Separate Caching of Retrieval and LLM Steps**: Since the retrieval step is not cached, only the LLM's input and output are stored in the cache, meaning any changes in the retrieved context will lead to a new LLM invocation.
- **Threshold Management**: It's crucial to set an appropriate similarity threshold for semantic caching. A high threshold ensures relevance but may lead to more cache misses.

---

## Summary and Resources

The video demonstrates how to implement MongoDB-based semantic caching for both simple LLM queries and RAG applications using LangChain. The examples help understand how caching can reduce costs but also highlight some challenges in managing semantic caching within RAG systems.

For more detailed information, refer to the documentation on:

- LangChain Documentation
- [MongoDB Atlas Documentation](https://www.mongodb.com/docs/atlas/)
- Exa Search Retriever Documentation
- [Anthropic Claude Models](https://www.anthropic.com/)

By understanding these concepts and code, you can implement a similar setup for caching LLM responses in your own projects.

 [[LLM]] [[LLM Frameworks]]  [[LangChain]]  [[Python]]