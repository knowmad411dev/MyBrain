---
tags:
- rag
- ollama
- pdf
video-url: https://www.youtube.com/watch?v=2TJxpyO3ei4&list=WL&index=2
---
### Python RAG Tutorial

This tutorial will guide you through the process of building a Retrieval-Augmented Generation (RAG) application using Python, Langchain, and ChromaDB. You will learn how to use PDFs as a knowledge base and integrate local language models to create a conversational AI that can provide intelligent answers based on document data.

### Setup Prerequisites:

To get started, make sure you have installed the necessary dependencies:

- **Langchain**: A library used to handle the different stages of document processing, such as loading, splitting, and embeddings.
- **ChromaDB**: A vector database to store and search through embeddings.
- **Embedding Models**: You will need an embedding model such as AWS Bedrock, OpenAI, or Ollama. Ollama is a good choice for local, open-source LLMs.

These libraries and models will help you process and structure your documents, making it possible for an LLM to understand and answer questions based on the documents.

### Loading Documents with Langchain:

1. **Document Loading Code**:
   ```python
   from langchain.document_loaders import PDFLoader
   
   loader = PDFLoader(path="data/")
   documents = loader.load()
   print(documents)
   ```
   - **Explanation**: First, you need to load your documents so they can be processed by your application. The `PDFLoader` in Langchain helps you load all PDF files from a specified folder (`data/`).
   - **Result**: This will load each document and create an object that contains the text content of the document along with some metadata, like page numbers and the document’s source.

### Splitting Documents into Chunks:

1. **Using Recursive Text Splitter**:
   - **Purpose**: The document might be too large to use effectively for embeddings. Splitting it into smaller parts (chunks) makes it easier for the model to process and create meaningful embeddings.
   - **How to Do It**: Use Langchain’s `RecursiveTextSplitter` to break the loaded document into smaller, manageable pieces. This splitter can intelligently divide content, taking care to not split sentences or phrases awkwardly, ensuring meaningful context in each chunk.

### Creating Embeddings and Vector Database:

1. **Embedding Function Setup**:
   - **Why Use Embeddings**: Embeddings are numerical representations of text that capture the semantic meaning. By creating embeddings, you can efficiently compare and search through your data using mathematical operations.
   - **Embedding Code**:
     ```python
     from langchain.embeddings import BedrockEmbeddings

     def create_embedding_function():
         return BedrockEmbeddings()
     ```
   - **Explanation**: This function uses AWS Bedrock as the embedding service. You can also choose other services like OpenAI or a local one, such as Ollama, depending on what works best for your setup.

2. **Consistency in Embedding Functions**:
   - **Why It’s Important**: Always use the same embedding function during both database creation and querying. This consistency ensures the generated embeddings are comparable, leading to successful and accurate searches.

3. **Vector Database Setup**:
   - **Purpose**: Store the embeddings in a vector database (e.g., ChromaDB), which allows you to perform fast and efficient searches for relevant content based on user queries.
   - **Storing Metadata**: Along with storing the text embeddings, you also store the metadata (source information, page numbers, etc.) to provide useful reference when generating answers.

### Adding and Updating Data in Vector Database:

1. **Unique ID Generation**:
   - **Why Assign Unique IDs**: Each chunk needs a unique identifier to manage additions and updates efficiently. This ensures you don't accidentally duplicate data.
   - **Generating IDs Code**:
     ```python
     from chromadb import Chroma

     database = Chroma(persist_directory="path/to/db")
     existing_ids = set(database.get_ids())

     for chunk in chunks:
         chunk_id = f"{chunk.source}-{chunk.page}-{chunk.index}"
         if chunk_id not in existing_ids:
             database.add(chunk, id=chunk_id)
     ```
   - **Explanation**: This code assigns a unique identifier to each chunk by combining the document path, page number, and chunk index. When new data is added, the database checks if the chunk already exists based on the ID, adding only the new ones.

### Running the RAG Application:

1. **Setting Up for Local Execution**:
   - **Load Functions and Data**: Create a Python script to load the embedding function, load the vector database, and prepare a prompt for the language model.
   - **Prepare Prompt Template**:
     ```python
     prompt_template = """
     Here is the information I found from the documents:
     {context}
     
     Question: {question}
     """
     ```
   - **Explanation**: The prompt template helps format the context (chunks retrieved from the database) and the user’s question. This prompt will be sent to the LLM to generate a response.

2. **Retrieving Context and Generating a Response**:
   ```python
   context = database.query(question, top_k=5)
   prompt = prompt_template.format(context=context, question=question)

   response = llm.generate(prompt)
   ```
   - **Explanation**: Use the vector database to find the top `K` chunks that best match the question. The selected chunks are then used as context in the final prompt, which is sent to the language model to generate the response.

### Testing and Evaluating the RAG Application:

1. **Why Testing Is Important**:
   - Ensuring that the generated responses are accurate is crucial, as response quality directly affects the usability of your application.
   - This tutorial uses unit tests to assess the response quality.

2. **Unit Testing with Pytest**:
   - **Writing Sample Questions**:
     ```python
     def test_monopoly_starting_money():
         question = "How much total money does a player start with in Monopoly?"
         expected_answer = "1500"
         actual_response = my_rag_app.query(question)
         assert llm_compare(expected_answer, actual_response)
     ```
   - **Explanation**: Unit tests compare the actual response from your RAG app with an expected answer. `pytest` is a popular Python testing framework that can be used to write these tests.

3. **LLM Evaluation of Responses**:
   - **LLM-Assisted Evaluation**: Since different phrasing may express the same correct answer, strict string comparison might fail even if the answer is accurate. Instead, use an LLM to judge equivalency.
   - **Negative Test Case**:
     ```python
     expected_response = "9999"
     actual_response = my_rag_app.query(question)
     assert llm_compare(expected_response, actual_response) == False
     ```
   - **Explanation**: Negative test cases ensure that incorrect responses are properly rejected by the evaluation mechanism. This kind of testing helps verify that the model doesn't pass incorrect results.

### Summary:

- **Dependencies and Setup**: Install necessary dependencies (`Langchain`, `ChromaDB`, embedding models) and gather your source documents.
- **Document Processing**: Use Langchain to load and split documents into smaller, workable chunks.
- **Creating Embeddings**: Use an embedding function to create vector representations for each document chunk and store them in a vector database (e.g., ChromaDB).
- **Application Workflow**: Load the embedding function and database, prepare prompts, query the database for relevant context, and pass the formatted prompt to the LLM to generate responses.
- **Testing Quality**: Write unit tests to evaluate the quality of generated responses and ensure correct and consistent performance as the data or model evolves.

This "Python RAG Tutorial" provides a step-by-step guide on building a retrieval-augmented generation system. It covers document processing, embedding, running the application locally, updating the vector database, and testing the entire application. With the provided code snippets and explanations, you can easily follow along to build your RAG app.

[[Ollama]]  [[RAG]]  [[Python]]  [[ChromaDB]]  [[LangChain]]