---
Video-URL: https://www.youtube.com/watch?v=lJOZiRoZNJw&list=WL&index=3
tags:
- ollama
- rag
- gpt
---

## **Chatbot - Llama 3.2 & Flowwise + Ollama

# Creating Local RAG Chatbot with Llama 3.2, Ollama, and Flowise

This tutorial will guide you through creating a free, local Retrieval-Augmented Generation (RAG) chatbot using Meta's newly released **Llama 3.2** model. You'll learn how to download and run the model locally using **Ollama** and build your chatbot using the open-source platform **Flowise**. By the end of this guide, you'll have a personalized AI assistant capable of accessing and understanding your custom knowledge base.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Step 1: Install Olama](#step-1-install-olama)
3. [Step 2: Download Llama 3.2 Model](#step-2-download-llama-32-model)
4. [Step 3: Download the Embeddings Model](#step-3-download-the-embeddings-model)
5. [Step 4: Install Node.js](#step-4-install-nodejs)
6. [Step 5: Install and Run Flowise](#step-5-install-and-run-flowise)
7. [Step 6: Create a Custom Knowledge Base](#step-6-create-a-custom-knowledge-base)
8. [Step 7: Add Documents to Your Knowledge Base](#step-7-add-documents-to-your-knowledge-base)
9. [Step 8: Configure the Vector Store](#step-8-configure-the-vector-store)
10. [Step 9: Create the RAG Chatbot](#step-9-create-the-rag-chatbot)
11. [Step 10: Build the Chatflow](#step-10-build-the-chatflow)
12. [Step 11: Test Your Chatbot](#step-11-test-your-chatbot)
13. [Additional Resources](#additional-resources)
14. [Conclusion](#conclusion)

---

## Prerequisites

- A computer with internet access
- Basic familiarity with command-line interfaces
- **Node.js** installed on your system

---

## Step 1: Install Olama

**Olama** allows you to run language models locally on your machine.

1. **Visit the Olama website**: [olama.com](https://olama.com)
2. **Download Olama** for your operating system (Windows, macOS, or Linux).
3. **Install Olama** by running the downloaded installer.
4. **Verify the installation**:

    Open your command prompt (Windows) or terminal (macOS/Linux) and run:

```bash
    olama
```

    If installed correctly, you should see a response from Olama.
    

---

## Step 2: Download Llama 3.2 Model

1. **Go back to Olama's website**: [olama.com](https://olama.com)
2. **Search for the Llama 3.2 model**:

    Use the search bar to find "llama 3.2".

3. **Select the 3-Billion Parameter Model**:

    Choose the 3B parameter model for this tutorial.

4. **Copy the Run Command**:

    You will see a run command associated with the model. Copy it.

```bash
    olama run llama-3b
 ```

5. **Download the Model**:

    Paste the run command into your command prompt or terminal and press **Enter**.

6. **Test the Model**:

    - After downloading, you can interact with the model.
    - Type a message like `Hello`.
    - If you receive a response, the model is working correctly.
7. **Exit the Interactive Prompt**:

```bash
    /bye
 ```

---

## Step 3: Download the Embeddings Model

You'll need an embeddings model to process your documents.

1. **Search for the Embeddings Model**:

    In your command prompt or terminal, run:

```bash
    olama search nomic-embed-text
 ```

2. **Copy the Run Command**:

    Find the appropriate run command for the **Nomic Embed Text** model and copy it.

```bash
    olama run nomic-embed-text
 ```

3. **Download the Model**:

    Paste and run the command to download the embeddings model.

---

## Step 4: Install Node.js

**Flowise** requires Node.js to run.

1. **Download Node.js**:

    Visit [nodejs.org](https://nodejs.org) and download the **LTS (Long-Term Support)** version.

2. **Install Node.js**:

    Run the downloaded installer and follow the prompts.

---

## Step 5: Install and Run Flowise

**Flowise** is an open-source platform for creating AI applications with a drag-and-drop interface.

1. **Open Command Prompt or Terminal**.
2. **Install Flowise**:

```bash
    npx flowise
  ```

    - When prompted to install the Flowise package, type `Y` and press **Enter**.
    - Installation may take about a minute.
3. **Start Flowise**:

```bash
    npx flowise start
 ```

4. **Access Flowise Interface**:

    Open your browser and go to `http://localhost:3000`.

5. **Enable Dark Mode** (Optional):

    For a better viewing experience, enable dark mode in the settings.

---

## Step 6: Create a Custom Knowledge Base

1. **Navigate to Document Stores**:

    In Flowise, go to the **Document Stores** section.

2. **Create a New Document Store**:

    - Click on **Create New Document Store**.
    - Name it (e.g., `Custom Knowledge Base`).
    - Click **Add**.

---

## Step 7: Add Documents to Your Knowledge Base

Prepare the documents you want to include, such as:

- A Word document (`.docx`) with FAQs or information.
- A CSV file with data (e.g., menu items and prices).

**To add documents:**

1. **Open Your Document Store**.
2. **Add Document Loader**:

    - Click on **Add Document Loader**.
    - Select the appropriate loader:
        - For Word documents: **Docx File**.
        - For CSV files: **CSV File**.
3. **Upload Your Document**:

    Choose the file from your computer.

4. **Preview and Split Documents** (for large files):

    - Under **Text Splitters**, select **Recursive Character Text Splitter**.
    - Set **Chunk Size** (e.g., `500` characters).
    - Set **Chunk Overlap** (e.g., `20` characters).
    - Click **Preview Chunks** to see the split.
    - This optimizes token usage by breaking documents into smaller pieces.
5. **Process the Document**:

    Click **Process** to load it into the document store.

6. **Repeat for Additional Documents**.

---

## Step 8: Configure the Vector Store

Your chatbot uses a vector database to retrieve relevant documents.

1. **Click on Upsert Config** in your document store.
2. **Select Embeddings Model**:

    - Choose **Olama Embeddings**.
    - Enter the model name (e.g., `nomic-embed-text`).
3. **Select Vector Store**:

    - Choose **FAISS** for this tutorial.
4. **Provide a Storage Path**:

    - Specify a folder path where the FAISS index will be stored.

        Example:

```bash

        C:\Users\YourName\Documents\VectorDB
 ```       
5. **Save Configuration**.
6. **Upsert Data**:

    Click **Upsert** to load documents into the vector database.

7. **Test Retrieval** (Optional):

    - Enter a sample query (e.g., `What are the current specials?`).
    - Verify that relevant documents are retrieved.

---

## Step 9: Create the RAG Chatbot

1. **Go to Chatflows** in Flowise.
2. **Add New Chatflow**:

    - Click **Add New**.
    - Name it (e.g., `My RAG Chatbot`).
    - Click **Save**.

---

## Step 10: Build the Chatflow

1. **Add Nodes to the Canvas**:

    - **Conversational Retrieval Chain**:
        - Found under **Chains**.
        - Handles conversation logic and document retrieval.
    - **Chat Olama**:
        - Found under **Chat Models**.
        - The language model that generates responses.
    - **Buffer Memory**:
        - Found under **Memory**.
        - Allows the chatbot to remember conversation history.
    - **Document Store**:
        - Found under **Vector Stores**.
        - Connects to your vector database.
2. **Connect the Nodes**:

    - **Chat Olama** → **Conversational Retrieval Chain**.
    - **Buffer Memory** → **Conversational Retrieval Chain**.
    - **Document Store** → **Conversational Retrieval Chain**.
3. **Configure Chat Olama Node**:

    - **Model Name**: Enter `llama-3b` (or the exact name from Olama).
        - You can list available models using:

```bash
            olama list
     ```
       
    - **Temperature**:
        
        - Controls response creativity (0 to 1).
        - Example: `0.6`.
4. **Configure Document Store Node**:
    
    - Select your document store from the dropdown (e.g., `Custom Knowledge Base`).
5. **Save the Chatflow**.
    

---

## Step 11: Test Your Chatbot

1. **Open the Chat Interface**:
    
    Click on the chat bubble icon.
    
2. **Interact with Your Chatbot**:
    
    - **Greet the Chatbot**:
        
        
```bash

        Hello
 ```       
    - **Ask a Knowledge-Based Question**:
        
        
```bash
        `What are your current specials?`
 ```       
        - The chatbot should respond with information from your documents.
    - **Ask Follow-Up Questions**:
        
        
```bash
        How much are your lamb chops?
 ```       
        - The chatbot uses memory to provide accurate answers.
3. **Modify Knowledge Base (Optional)**:

    - Add or remove documents in your document store.
    - Remember to **Upsert Config** and **Upsert** to update the vector database.

---

## Additional Resources

- **Olama Website**: [olama.com](https://olama.com)
- **Node.js Download**: [nodejs.org](https://nodejs.org)
- **Flowise GitHub Repository**: [github.com/FlowiseAI/Flowise](https://github.com/FlowiseAI/Flowise)
- **Flowise Documentation**: [flowiseai.com](https://flowiseai.com)
- **Tutorial on Using Olama**: _(Refer to Olama's official tutorials or documentation)_

---

## Conclusion

You've successfully created a local RAG chatbot using **Llama 3.2**, **Ollama**, and **Flowise**. Your chatbot can now access and understand your personal documents, providing accurate and context-aware responses. Feel free to expand your knowledge base by adding more documents or experimenting with different models and settings.

[[RAG]]  [[Ollama]]    [[GPT]]