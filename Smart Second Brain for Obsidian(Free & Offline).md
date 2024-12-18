---
tags:
- obsidian
---
## **Overview of the AI-Powered Obsidian Integration

This guide explains how to integrate **local, privacy-friendly AI** into **Obsidian** to transform it into a personal AI assistant. The AI can chat with you, answer questions, and brainstorm ideas using your notes as context. Importantly, this works completely **offline** and is **free**, ensuring privacy and security.

The setup involves installing:

1. A **local AI application** (Ollama)
2. The **Smart Second Brain** plugin in Obsidian

By the end, you can interact with AI that processes and retrieves information directly from your knowledge base.

---

## Step 1: Installing the Local AI Application (Ollama)

To run AI models offline, you need **Ollama**, an application that allows you to manage large language models (LLMs) locally.

1. **Download Ollama**
    
    - Open your browser and search for **Ollama**.
    - Go to [https://ollama.com](https://ollama.com/).
    - Download the application for your operating system (Windows, Mac, or Linux).
2. **Install Ollama**
    
    - On Mac:
        - Unzip the downloaded `.zip` file.
        - Move the `Ollama` application to your Applications folder.
    - On Windows:
        - Run the installer and follow the setup instructions.
    - On Linux:
        - Use the package manager instructions provided on the Ollama website.
3. **Launch Ollama**
    
    - Open the Ollama app to ensure it is running.

---

## Step 2: Install the Smart Second Brain Plugin in Obsidian

To integrate Ollama with Obsidian, use the **Smart Second Brain** plugin.

1. **Open Obsidian**.
2. Go to **Settings** > **Community Plugins**.
3. Enable **Safe Mode** (if not already done).
4. Search for **Smart Second Brain**.
5. Click **Install** and then **Enable**.

---

## Step 3: Configure the Smart Second Brain Plugin

Once the plugin is installed:

1. Open **Settings** > **Smart Second Brain**.
    
2. Configure the following options:
    
    - **Auto-start**: Enable it to automatically start the plugin when Obsidian opens.
    - **Exclude Files/Folders**: Exclude specific files or folders to speed up indexing.
3. Under **AI Integration**, select **Ollama** as the backend.
    
    - Choose your desired **Language Model** (e.g., `LLaMA2`, `Mistral`, `Gemma`).
    - Select the **Embedding Model** (e.g., `mxbai-embed-large` for best results).
4. Save the settings.
    

---

## Step 4: Download and Configure a Language Model

To use Ollama, you need to download a language model:

1. **Open Ollama** and navigate to the **Models** section.
2. Choose a model (e.g., `LLaMA2`, `Mistral`, or `Gemma`).
3. Copy the terminal command provided for the model.
    - Example: `ollama pull llama2`.
4. Open your terminal, paste the command, and press Enter to download.
    - Model file sizes can range from **5GB** (e.g., `Gemma`) to **25GB** (e.g., `Mixtral`). Ensure you have sufficient resources.
5. Once downloaded, return to Obsidian and test the model connection:
    - Open **Command Palette** (Ctrl/Cmd+P).
    - Search for **Smart Second Brain** > **Test Connection**.

---

## Step 5: Index Your Obsidian Vault

1. Once the language and embedding models are set, go to **Smart Second Brain** settings.
2. Click **Reinitialize** to start indexing your notes.
3. Depending on the size of your vault, indexing may take several minutes.
4. To improve indexing speed, exclude unnecessary files and folders.

---

## Step 6: Interact with Your Personal AI

With everything set up, you can now chat with the AI:

1. Open the **Command Palette** and search for **Smart Second Brain: Open Chat**.
    
2. A chat window will open.
    
3. **Toggle Context Mode**:
    
    - **Octopus Icon OFF**: The AI responds based on its pre-trained knowledge.
    - **Octopus Icon ON**: The AI uses your indexed notes as context.
4. **Ask Questions**:
    
    - Example: "What is the 100-hour rule?"
    - If no notes are retrieved, lower the **Similarity Threshold** in settings.
5. **Advanced Controls**:
    
    - **Similarity Threshold**: Determines how closely the AI searches for matching notes.
    - **Creativity Level**: Adjusts the randomness of responses.

---

## Best Language Model and Embedding Model Combinations

The plugin creator recommends:

- **Chat Model**: `LLaMA2` or `Mistral` (lighter models for most systems).
- **Embedding Model**: `mxbai-embed-large` for accurate indexing and retrieval.

For powerful PCs:

- Use **Mixtral** (25GB model) for results comparable to GPT-3.5.

---

## Troubleshooting Common Issues

1. **AI Returns "No Notes Retrieved"**:
    
    - Lower the **Similarity Threshold** (e.g., set to 30-50%).
    - Ensure your notes are indexed properly.
2. **Long Indexing Times**:
    
    - Exclude unnecessary files/folders in the plugin settings.
    - Use smaller embedding models for faster performance.
3. **AI Creates Links to Non-Existent Notes**:
    
    - This is a known limitation and may improve with future updates.

---

## Saving and Managing Chats

1. **Save Chats**:
    
    - You can save conversations as notes within your vault for future reference.
2. **New Chat**:
    
    - Start a new chat by clearing the current chat window.
3. **Delete Chats**:
    
    - Use the trash icon to remove old conversations.

---

## Summary

By integrating Ollama and the Smart Second Brain plugin, you can transform Obsidian into a powerful AI-powered assistant. This system works offline, respects your privacy, and leverages your notes to provide tailored insights.

**Recommended Configuration:**

- **Chat Model**: `LLaMA2`
- **Embedding Model**: `mxbai-embed-large`

For high-performance systems, try **Mixtral** for GPT-3.5-level responses.

With this setup, you now have a **free, offline AI assistant** ready to help you process, summarize, and brainstorm using your personal knowledge base.

[[Obsidian]]