---
tags:
- llamaindex
- python
video-url: https://www.youtube.com/watch?v=cCyYGYyCka4&list=WL&index=2
---
## **Introduction to LlamaIndex with Python

Good morning, everyone! Today, we're diving into Lama Index, a framework for working with large language models (LLMs). Lama Index provides tools to create LLM-based applications, such as chatbots, AI assistants, translation systems, and more. It allows you to connect unstructured data like emails, PDFs, or databases to language models, making them more knowledgeable about your specific content. Let’s break down the key components of Lama Index and how to use them step-by-step.

### What is Lama Index?

Lama Index (often abbreviated as L Index) is a framework or ecosystem that supports the creation of LLM-based applications, similar to LangChain. However, it includes unique features like specialized data loaders and tools to create sophisticated AI agents. The framework helps augment LLMs by enriching their knowledge with structured and unstructured data from your own sources, such as emails, company databases, or note-taking apps.

### Key Components of Lama Index

1. **Data Connectors**: These are tools that ingest structured and unstructured data from various formats, including PDF, HTML, CSV, and Word documents. Lama Index offers sophisticated data connectors that can handle multiple document types and create structured versions for use in your LLM application.
2. **Documents**: After ingestion by data connectors, the data is converted into documents. These documents are not PDF or Word files but are instead programming objects containing text and metadata, such as the source file name, page numbers, and ingestion date.
3. **Nodes**: Documents are split into smaller chunks called nodes, which retain the metadata from the document. These nodes are interconnected, forming a network of knowledge that the LLM can reference. This approach is different from LangChain, as Lama Index explicitly focuses on nodes and their interconnected nature.
4. **Embeddings and Index**: Nodes are transformed into numerical representations (embeddings) using an embedding model. These embeddings are stored in an index, which is a vector database containing all the node embeddings. The index allows efficient querying of your data.
5. **Router and Retriever**: When a user makes a query, the **Router** decides which **Retriever** to use to gather the relevant information from the index. The **Retriever** finds the appropriate nodes, and the **Response Synthesizer** combines these nodes with a prompt and passes them to the language model for a response.

### How to Get Started with Lama Index

To start using Lama Index, follow these steps:

1. **Install Lama Index**: Run the following command to install Lama Index:
   ```bash
   pip install lama-index -Uq
   ```

   The `-Uq` options upgrade the package and suppress unnecessary output.

2. **Set Up OpenAI API Key**: Lama Index uses OpenAI's language models by default, specifically GPT-3.5-turbo, which is inexpensive and powerful. Set your API key using:
   ```python
   import openai
   openai.api_key = 'YOUR_OPENAI_API_KEY'
   ```

3. **Ingest Data**: Create a folder named `data` to store documents for ingestion. For example, you can place `constitution.pdf` in this folder. Lama Index uses `SimpleDirectoryReader` to load documents from this directory.
   ```python
   from llama_index import VectorStoreIndex, SimpleDirectoryReader
   documents = SimpleDirectoryReader('data').load_data()
   index = VectorStoreIndex.from_documents(documents)
   ```

4. **Query Your Data**: Convert the index into a query engine and ask questions about your data.
   ```python
   query_engine = index.as_query_engine()
   response = query_engine.query('What is the first article of the Constitution?')
   print(response)
   ```

### Persistent Storage with Lama Index

If you want to persist your data across sessions (so you don’t have to re-ingest documents every time), you can use `StorageContext`. This makes the vector database persistent on your local machine:

```python
from llama_index import VectorStoreIndex, SimpleDirectoryReader, StorageContext
import os

persist_dir = 'storage'
if not os.path.exists(persist_dir):
    documents = SimpleDirectoryReader('data').load_data()
    index = VectorStoreIndex.from_documents(documents)
    index.storage_context.persist(persist_dir)
else:
    storage_context = StorageContext.from_defaults(persist_dir=persist_dir)
    index = VectorStoreIndex.load_from_storage(storage_context)

query_engine = index.as_query_engine()
response = query_engine.query('What is the third article of the Constitution?')
print(response)
```

This script checks if the storage directory exists, and if it does, it loads the stored index, allowing you to save time during subsequent runs.

### Using Lama Pars

For more complex document types (e.g., those containing tables or images), you can use **Lama Pars**, a cloud-based service by Lama Index that converts documents into structured text via an API. Sign up at [lamac.cloud](https://lama.cloud) and obtain an API key to use this feature.

Replace `SimpleDirectoryReader` with `LamaPars` to ingest documents using this API. Remember to set your Lama Cloud API key:

```python
from lama_pars import LamaPars
import os

os.environ['LAMACLOUD_API_KEY'] = 'YOUR_LAMA_CLOUD_API_KEY'
lamapars = LamaPars()
documents = lamapars.load_data('data/constitution.pdf')
```

Lama Pars works well for more complicated files with mixed content, providing cleaner and more usable text for your LLMs.

### Summary

Lama Index provides a powerful ecosystem for creating LLM applications, with tools for ingesting data, managing it, and allowing language models to interact with the data. Its features, like data connectors, nodes, embeddings, and specialized tools like Lama Pars, make it an invaluable resource for building sophisticated AI solutions.

Stay tuned for future videos in this series, where we will dive deeper into more advanced features of Lama Index. If you have any questions or suggestions, feel free to leave them in the comments. Thanks for watching!

----

In this lesson, we will go through an introduction of LlamaIndex. We will see what you can do with it, how it deals with RAG and its main components. We will then implement a RAG pipeline with their famous 5-liner, which allows you to chat with your data in 5 lines of code. This tutorial is based on the original [LlamaIndex documentation](https://docs.llamaindex.ai/en/stable/).

<iframe src="https://www.youtube.com/embed/cCyYGYyCka4" allowfullscreen="" title="YouTube Video"></iframe>

## What is LlamaIndex?[#](https://alejandro-ao.com/intro-to-llamaindex/#what-is-llamaindex)

LlamaIndex is a Python library that allows you to build a search engine for your documents. It is designed to be simple to use and easy to integrate with your existing code.

![LlamaIndex RAG Pipeline](https://alejandro-ao.com/intro-to-llamaindex/llamaindex-rag-pipeline_huab6414989d32b70d840e3cec87d1f311_578005_660x0_resize_box_3.png)

## Installation and Setup[#](https://alejandro-ao.com/intro-to-llamaindex/#installation-and-setup)

To install LlamaIndex, you can use pip:

```bash
%pip install -Uq llama-index
```

LlamaIndex uses OpenAI’s models by default (both for embeddings and LLM), so you will need an API key to use it. You can get an API key by signing up for an account on the [OpenAI website](https://beta.openai.com/signup/). Once you have an API key, you can set it as an environment variable in your code:

```python
import getpass import os os.environ['OPENAI_API_KEY'] = getpass.getpass("OpenAI API Key: ")
```

## Getting Started[#](https://alejandro-ao.com/intro-to-llamaindex/#getting-started)

To get started with LlamaIndex, you first need to create a `VectorStoreIndex` object. This object will store the documents you want to search through. You can create a `VectorStoreIndex` object from a list of documents.

```python
from llama_index.core import VectorStoreIndex, SimpleDirectoryReader documents = SimpleDirectoryReader("data").load_data() index = VectorStoreIndex.from_documents(documents) query_engine = index.as_query_engine() response = query_engine.query("What is the first article?") print(response)
```

Note that we are using `SimpleDirectoryReader`. This reader will load any file it finds in a given directory. It is capable of ingesting the following formats:

-   .csv - comma-separated values
-   .docx - Microsoft Word
-   .epub - EPUB ebook format
-   .hwp - Hangul Word Processor
-   .ipynb - Jupyter Notebook
-   .jpeg, .jpg - JPEG image
-   .mbox - MBOX email archive
-   .md - Markdown
-   .mp3, .mp4 - audio and video
-   .pdf - Portable Document Format
-   .png - Portable Network Graphics
-   .ppt, .pptm, .pptx - Microsoft PowerPoint

For more information on `SimpleDirectoryReader`, you can visit the [official documentation](https://docs.llamaindex.ai/en/stable/module_guides/loading/simpledirectoryreader/).

## Persisting the Index[#](https://alejandro-ao.com/intro-to-llamaindex/#persisting-the-index)

You can persist the index to disk so that you can load it later without having to re-index your documents. `VectorStoreIndex` has a `persist` method that allows you to save the index to disk. You can then load the index from disk using the `load_index_from_storage` function. Here is an example:

```python
import os.path from llama_index.core import ( VectorStoreIndex, SimpleDirectoryReader, StorageContext, load_index_from_storage, ) 
# check if storage already exists 
PERSIST_DIR = "./storage" if not os.path.exists(PERSIST_DIR): 
# load the documents and create the index 
documents = SimpleDirectoryReader("data").load_data() index = VectorStoreIndex.from_documents(documents) 
# store it for later 
index.storage_context.persist(persist_dir=PERSIST_DIR) else: 
# load the existing index 
storage_context = StorageContext.from_defaults(persist_dir=PERSIST_DIR) index = load_index_from_storage(storage_context) 
# Either way we can now query the index 
query_engine = index.as_query_engine() response = query_engine.query("What is the third article about?") print(response)
```

## LlamaParse[#](https://alejandro-ao.com/intro-to-llamaindex/#llamaparse)

We can also load our documents using LlamaIndex’s API, which automates the extraction of more complicated documents:

```python
# LlamaParse is async-first, so we need to run this line of code if you are working on a notebook import nest_asyncio nest_asyncio.apply()
```

Set up your API key:

```python
import getpass import os os.environ["LLAMA_CLOUD_API_KEY"] = getpass.getpass()
```

Now you can use LlamaParse to load your documents:

```python
from llama_index.core import VectorStoreIndex, SimpleDirectoryReader from llama_parse import LlamaParse documents = LlamaParse(result_type="text").load_data("./your-file.whatever") index = VectorStoreIndex.from_documents(documents) query_engine = index.as_query_engine() response = query_engine.query("What is the first article?") print(response)
```

## Conclusion[#](https://alejandro-ao.com/intro-to-llamaindex/#conclusion)

In this lesson, we learned about LlamaIndex, a Python library that allows you to build a search engine for your documents. We saw how to install and set up LlamaIndex, how to get started with it, and how to persist the index to disk. We also learned about LlamaParse, which automates the extraction of more complicated documents. In the next lesson, we will see how to use LlamaIndex to build a RAG pipeline.

[[LlamaIndex Framework]]  [[Python]]  