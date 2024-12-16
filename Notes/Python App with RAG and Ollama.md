---
tags:
- ollama
- python
- rag
- chromadb
---

## **Building a Basic Retrieval-Augmented Generation (RAG) System with Python and Chroma DB**

### Overview

This tutorial focuses on setting up a **Retrieval-Augmented Generation (RAG)** system using **Python** and **Chroma DB**, a vector database designed to support **embedding** and similarity searches. A RAG system allows users to ask questions to documents, such as Markdown files, web pages, or PDFs. The goal is to provide precise answers by retrieving only relevant fragments of documents rather than confusing the model with entire documents.

The tutorial covers how to split documents, create embeddings, and store them in Chroma DB for efficient similarity search. Python is used throughout this tutorial, with a Typescript version promised in a future companion video.

### Key Concepts

1. **Retrieval-Augmented Generation (RAG)**: A RAG system combines a language model with a database of documents, allowing the model to generate more informed responses based on the embedded documents.
2. **Embeddings**: Embedding is a process where text is transformed into numerical arrays that capture the meaning and context of the original text, making similarity searches possible.
3. **Chroma DB**: This is the vector database used for storing document embeddings and supporting similarity searches. It is simple, fast, and ideal for setting up a basic RAG system.

### Setting Up Chroma DB

1. **Install Chroma DB** and run an instance:

   ```sh
   chroma run --host localhost --port 8000 --path my_chroma_data
   ```

   This command sets up a Chroma DB instance on localhost with the specified path for storing data.

2. **Connect to Chroma DB from Python**: Create a Python script to connect to Chroma DB, delete existing collections, and create a new collection for embeddings:

   ```python
   from chromadb import ChromaClient

   client = ChromaClient()
   # Delete collection if it exists
   if client.collection_exists("my_collection"):
       client.delete_collection("my_collection")
   # Create a new collection
   collection = client.create_collection("my_collection")
   ```

### Preparing Source Documents

1. **Source Files**: Prepare a text file called `source_docs.txt` that lists the **URLs** or **file paths** for documents to be embedded. The example uses a list of articles from the **Mac Rumors** website.
2. **Download Files**: Retrieve the text from each URL or file. Use a custom function, `retext()`, to extract the article's text content.

### Chunking the Text

1. **Chunking**: Chunking is the process of splitting large text documents into smaller, manageable pieces (chunks).
   - The tutorial uses **sentence-based chunking** by leveraging the `nltk` library's `sent_tokenize` function:
   ```python
   from nltk.tokenize import sent_tokenize

   def chunk_text_by_sentence(text, num_sentences=3):
       sentences = sent_tokenize(text)
       return [" ".join(sentences[i:i + num_sentences]) for i in range(0, len(sentences), num_sentences)]
   ```
   - Each chunk will consist of a configurable number of sentences, making it easier for embeddings to capture the text's meaning.

### Creating Embeddings

1. **Embedding Models**: The video suggests three models for creating embeddings in Ollama (as of April 2024):

   - **namc\_embed\_text**
   - **mxb\_AI\_embed\_large** (Mix Bread model)
   - **all-mini-LM**
   - In the tutorial, **namc\_embed\_text** is preferred due to its speed and quality.

2. **Generate Embeddings**: Generate embeddings for each chunk:

   ```python
   from olama_tools import embed_text

   def create_embeddings(chunks, model_name="namc_embed_text"):
       embeddings = []
       for chunk in chunks:
           embedding = embed_text(model_name=model_name, text=chunk)
           embeddings.append(embedding)
       return embeddings
   ```

### Adding to Chroma DB

1. **Store Embeddings**: For each chunk, store the embedding in Chroma DB, along with metadata, such as the **source document's name** and the **index** of the chunk.
   ```python
   for i, embedding in enumerate(embeddings):
       collection.add(
           embeddings=[embedding],
           metadatas=[{"source": source_file, "chunk_index": i}],
           ids=[f"{source_file}_{i}"]
       )
   ```

### Performing a Search

1. **Initialization**: Start by reading the **model names** from the configuration file, and **connect** to the Chroma DB instance.
2. **Create Embedding for Query**: Use the CLI to provide a query and create its embedding:

   ```python
   query_embedding = embed_text(model_name=model_name, text=query)
   ```

3. **Run Query**: Use Chroma DB to find the top matching results for the query:

   ```python
   results = collection.query(query_embedding, top_k=5)
   combined_text = " ".join(result["text"] for result in results)
   ```

4. **Send to Language Model**: Combine the original query with the retrieved documents and send it to the LLM:

   ```python
   response = olama.generate(
       model_name="dolphin_mistl",
       prompt=f"{query}\n\n{combined_text}",
       stream=True
   )

   for part in response:
       print(part)
   ```

### Running the System

1. **Importing Articles**: Run the script to import all articles:

   ```sh
   python3 import.py
   ```

   This will read from `source_docs.txt` and add the chunks to Chroma DB.

2. **Perform a Search**: Run a query on the imported articles:

   ```sh
   python3 search.py "What happened in Taiwan?"
   ```

   The model will return a description of the recent **earthquake in Taiwan** and its impact on **TSMC**.

3. **Switching Models**: You can easily change models, both for embedding and for generation, using the configuration file:

   - **Main Model**: Switch to **Gemma: 2B** and try different queries to see how each model performs.

### Advanced Use Cases

- **Add Metadata**: Include additional metadata, like the **date** of the article, to prioritize recent information when answering queries.
- **Dynamic Search**: Perform a real-time search on a website, embed the top five results, and then do a similarity search with the model.

### Conclusion

This tutorial provides a basic setup for a RAG system using **Chroma DB** and **Python**. You can expand the system by adding dynamic capabilities, such as sorting by date or importing real-time data. The code is available in the **techno evangelist video projects GitHub repo**. If you have questions or ideas for future videos, join the discussion on Discord or leave a comment.

**Note**: PDFs, while commonly used, are not ideal for this process due to difficulties in extracting clean text. Future videos will explore better workflows for converting PDFs to usable text.

[[Python]]   [[Ollama]]   [[RAG]]   [[ChromaDB]]
