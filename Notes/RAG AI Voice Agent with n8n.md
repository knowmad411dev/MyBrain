---
tags:
- rag
- agents
- speech
- automation
video-url: https://www.youtube.com/watch?v=NB7hMj7pfrA&list=WL&index=1
---
## **RAG AI Voice Agent with n8n

### **Overview

The tutorial covers building a **Retrieval-Augmented Generation (RAG) voice AI assistant** for a website using **N8N**, an open-source automation tool. This voice assistant accesses data from documents and a website to answer user queries in a personalized manner, converting user speech to text, generating a response, and sending it back as audio. It's a budget-friendly solution, ideal for individuals or small businesses.

### **Workflow Overview**

The entire project is broken into three key workflows:

1. **Embedding Workflow**: Extracts content from documents and stores it in a vector database.
2. **Voice Query Handling Workflow**: Converts user speech to text, processes it, and returns responses in audio format.
3. **WordPress Plugin Integration**: Creates a website interface for interaction with the assistant.

Let’s dive into each workflow in detail.

### **Step 1: Setting Up Vector Database and Embedding Workflow**

This workflow pulls data from documents, breaks it into smaller chunks, and stores them as embeddings for easy retrieval.

1. **Create a Google Drive Directory**
   - Create a folder called **test_docs** in Google Drive and add the document with information that the assistant will use (e.g., business details and services).

2. **Configure N8N Workflow**
   - Use **N8N** to set up an automated workflow.
   - Add a **Google Drive node** that triggers on changes (e.g., whenever files are added/modified in the folder).

3. **Connect Google Drive API**
   - Navigate to **console.cloud.google.com** and **search for Google Drive API**.
   - Enable the API, create an application using the **OAuth consent screen**, and add the domain for N8N under **authorized domains**.
   - Publish the app and generate **OAuth credentials** (client ID and client secret) for N8N.

4. **Download the Document**
   - Add a second **Google Drive node** to **download the file** once it’s detected.
   - Use an **iterator node** to handle multiple files if needed.

5. **Generate Embeddings with Pinecone**
   - Break down the document into chunks using a **Recursive Character Text Splitter**.
   - Use **Pinecone** as the vector store to store the embeddings.
     - Set up a Pinecone index and generate an **API Key**.
     - Add this key to N8N as a credential.
     - Use **OpenAI embeddings** to convert chunks to vector representations.
     - Add metadata like the filename to enhance search efficiency.

### **Step 2: Handling Voice Queries Workflow**

This workflow lets the assistant receive voice queries, generate responses, and return them as audio.

1. **Webhook Node in N8N**
   - Add a webhook node to receive user queries via voice from the website.
   - Set the **method type** to **POST** and set authentication as needed.

2. **Transcribe User Input**
   - Use **OpenAI** to **transcribe** audio into text for further processing.

3. **Query the Vector Database**
   - Add an **AI Agent** to prepare the response.
   - Use a **session key** to maintain context.
   - Define a **system message** for how the assistant should behave (e.g., “You are a voice assistant for Green Globe Wellness Retreat…”).
   - Add a **tool** to query Pinecone for relevant embeddings.

4. **Convert Text to Audio**
   - Use **OpenAI text-to-speech** to generate an audio response.
   - Set the model (e.g., **tds1**) and choose a voice style.

5. **Send Audio Response**
   - Add a **Respond to Webhook Node** to send the audio back to the website.
   - Set the response format as **Binary File** since it’s an audio file.

### **Step 3: WordPress Plugin Integration**

Integrate the AI assistant into the website to create a seamless interaction.

1. **Create a WordPress Plugin**
   - Create a directory called **voice_chat_widget** in WordPress’s **plugins** folder.
   - Include three files:
     1. **voice_chat_widget.php**: Displays the chat button on the website.
     2. **voice_chat.css**: Controls the styling of the chat widget.
     3. **voice_chat.js**: Contains JavaScript logic for recording audio, detecting voice activity, stopping the recording, and processing the response.
   - Use an **init function** to generate a **unique session ID** for each user, which will be used in every webhook call.

2. **Activate the Plugin**
   - Go to **WordPress > Plugins** and activate the **Voice Chat Widget** plugin.
   - Once activated, the widget button will appear on the website.

3. **Testing the Workflow**
   - Start a conversation by clicking the widget button on the website.
   - Example query: “Are you open this Thursday?” The AI will respond (e.g., “Yes, we are open from 6:00 AM to 10:00 PM”).
   - Use N8N’s debug view to verify the data flow through each node (e.g., checking if the vector store fetched relevant embeddings).

### **Key Code Examples and How-Tos**

1. **Google Cloud OAuth Setup**
   ```plaintext
   - Go to console.cloud.google.com > Google Drive API
   - Enable API > OAuth Consent Screen > Create Application > Add name, authorized domains > Save > Create Credential
   - Generate OAuth Client ID > Type: Web Application > Add Redirect URI (from N8N)
   - Copy Client ID and Secret to N8N.
   ```

2. **Text Chunking and Embedding Generation**
   ```python
   # Pseudocode for breaking down text and generating embeddings
   file = download_file_from_google_drive()
   chunks = recursive_character_splitter(file, chunk_size=1000, overlap=200)
   embeddings = openai_embedding_model(chunks)
   pinecone_store.add(embeddings, metadata={'filename': 'business_info.doc'})
   ```

3. **JavaScript for Voice Widget**
   ```javascript
   function init() {
       // Generate unique session ID for each user
       sessionId = generateUniqueSessionID();
       // Additional initialization logic for chat button
   }

   function startRecording() {
       // Set up audio recording with voice detection
   }

   function stopRecording() {
       // Process the audio and send it to the webhook
   }

   function playResponse(audio) {
       // Play audio response from AI assistant
   }
   ```

4. **PHP for WordPress Plugin Activation**
   ```php
   <?php
   /*
   Plugin Name: Voice Chat Widget
   Description: Adds a voice chat button to interact with the AI Assistant.
   Version: 1.0
   */

   function add_voice_chat_button() {
       echo '<div id="voice-chat-widget"></div>'; // Add the button to the website
   }
   add_action('wp_footer', 'add_voice_chat_button');
   ?>
   ```

### **Tips and Best Practices**

1. **Optimize Memory Usage**:
   - Use external memory solutions instead of **Window Buffer Memory** for large workflows to prevent system crashes.

2. **Session Management**:
   - Ensure each user gets a **unique session ID** to keep conversations consistent and context-aware.

3. **Error Handling**:
   - Implement error handling for API issues to provide user feedback, like “I’m currently unable to answer, please try again later.”

4. **Scalability and Additional Tools**:
   - Add tools such as a **calendar tool** for scheduling appointments to increase the assistant’s capabilities.

### **Summary**

In this tutorial, you built a **voice AI assistant** using **N8N**, **Google Drive**, **Pinecone**, and **OpenAI** to create an engaging experience for website visitors. The assistant converts voice to text, searches through stored documents using vector embeddings, and responds in audio format. The WordPress integration makes it accessible to users with a simple chat button, demonstrating how automation tools and AI can work together to build powerful, interactive, and cost-effective solutions.

[[RAG]]  [[AI Voice Assistants]]  [[N8N Masterclass]]  [[Workflow]]  