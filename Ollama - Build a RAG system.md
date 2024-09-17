# Let's build a RAG system - The Ollama Course
https://www.youtube.com/watch?v=FQTCLOUnIzI

![](https://www.youtube.com/watch?v=FQTCLOUnIzI)
## Summary:

- 📋 **Overview of RAG**: The video introduces **Retrieval Augmented Generation (RAG)**, explaining how it involves embedding and retrieval to improve AI models' answers by pulling relevant information from external sources.
- 💻 **Tasks to build a RAG system**: Step-by-step guide to setting up a RAG system, covering environment setup, document embedding, and querying the database.
- 🛠️ **Python and Typescript examples**: Shows examples of using Python and Typescript to create a basic RAG system.
- 🐍 **Using Python**: Step-by-step instructions for importing text documents, chunking them, embedding them, and storing them in a **Chroma** vector database.
- 🖥️ **Typescript and Dino**: Parallel demonstration of the same process using **Typescript** and **Dino** for embedding and querying data.
- 🌐 **Pre-built RAG solutions**: Mentions several pre-built tools, including **Open Web UI** and **Misty Page**, which offer ready-to-use RAG systems.
- 🧑‍💻 **Chroma and Docker**: Detailed instructions on setting up **Chroma** with Docker to manage data storage for the RAG system.

### Steps to Build a RAG (Retrieval Augmented Generation) System

1. **Set Up the Environment**:
    
    - The primary task is to configure the environment for a vector database. In this example, the chosen database is **Chroma**.
    - You can use **Chroma** either as a hosted service or as a self-hosted solution.
    - The easiest way to run Chroma locally is by using **Docker**. Run the following Docker command to launch Chroma:
        
        bash
        
        Copy code
        
        `docker run -dp 8000:8000 chromadb/chroma`
        
2. **Add Text Data to the Database**:
    
    - You need a set of documents or text data that the system can retrieve from. Here, the text is chunked into small parts for better retrieval.
    - Organize your documents in a directory. Each document will be chunked, and its metadata, like the file name, will be included.
3. **Python Implementation**:
    
    - In Python, follow these steps to add documents to Chroma:
    - **Set up Chroma Client**: Use the Chroma API to create a collection in which your data will be stored.
    - **Chunk the Text**: Split each document into chunks, typically around **100 words** each.
    - **Embedding and Metadata**: Each chunk will be embedded using a vector embedding model, along with metadata like the document's source file.
    - **Add to Chroma Database**: Insert the chunks and metadata into the Chroma database.
    - Example Python code to import documents:
        
        python
        
        Copy code
        
        `from chromadb import Client client = Client() collection = client.create_collection("my_documents")  # Function to add documents def add_documents():     for doc in documents:         chunks = chunk_text(doc)         embeddings = embed(chunks)         collection.add(chunks, embeddings, metadata)`
        
4. **Verify Database Insertion**:
    
    - You can verify that the documents were successfully added to the Chroma database by visiting the Chroma API endpoint at **localhost:8000/docs**.
    - Try retrieving the added documents using the collection ID.
5. **Typescript Implementation**:
    
    - In Typescript, a similar approach is used:
        - **Set up Chroma Client**: Initialize Chroma and create a collection.
        - **Chunk the Text**: Same as Python, split each document into chunks.
        - **Embed the Chunks**: Embed the chunks using a vector model.
        - **Add to Chroma Database**: Add chunks and their embeddings to the Chroma collection.
    - Example Typescript code:
        
        typescript
        
        Copy code
        
        `import { Client } from 'chroma'; const client = new Client(); const collection = client.createCollection('my_documents');  // Function to add documents function addDocuments() {     documents.forEach(doc => {         const chunks = chunkText(doc);         const embeddings = embed(chunks);         collection.add(chunks, embeddings, metadata);     }); }`
        
6. **Query the Database**:
    
    - Once the documents are embedded in Chroma, you can perform queries using embeddings. The system retrieves relevant document chunks based on the input query.
    - In Python or Typescript, query the database with the embedded query and retrieve the results.
    - Example query in Python:
        
        python
        
        Copy code
        
        `results = collection.query(query_embedding) print(results)`
        
7. **Generate a Response**:
    
    - The retrieved chunks are combined to form a prompt, which is then sent to the language model (e.g., GPT-3) to generate a response.
    - You can compare the response with and without RAG to see the improvement in the relevance of the answers.

By following these steps, you will have a simple RAG system up and running with Chroma as your vector database and either Python or Typescript to manage embeddings and queries.
