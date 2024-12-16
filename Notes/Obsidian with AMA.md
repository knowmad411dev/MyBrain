---
Video-URL: https://www.youtube.com/watch?v=9YYB8a_ehc4&list=WL&index=2
tags:
- obsidian
- llm
---

## **Obsidian with AMA**

### Detailed Summary: Using AMA for Local Large Language Models (LLMs) in Obsidian

In this video, the presenter addresses concerns about data privacy when using cloud-based AI services like ChatGPT for managing notes in Obsidian. To mitigate these concerns, the video introduces **AMA**, an open-source project that allows users to run local Large Language Models (LLMs) on their machines. This ensures that your notes remain private, as data isn't sent to third-party cloud services. Below is a comprehensive summary of the video, including step-by-step instructions and relevant commands.

---

#### **1. Introduction**

- **Problem Statement:** Utilizing cloud-based AI services (e.g., ChatGPT) for note-taking in Obsidian compromises data privacy, as your notes are sent to external servers.
- **Solution:** Use **AMA** to run local LLMs on your machine, ensuring data privacy while still leveraging AI capabilities within Obsidian.

---

#### **2. Understanding Key Terms**

- **Local LLM (Large Language Model):** Refers to running models like LLaMA 2, LLaMA 3, Mistral locally on your machine or server, rather than accessing them via cloud APIs.
- **AMA:** An open-source project that simplifies the process of downloading, managing, and running local LLMs. It supports models such as LLaMA 2, LLaMA 3, Mistral, etc., and is free to use.

---

#### **3. Advantages of Using Local LLMs with AMA**

- **Data Privacy:** No need to send your notes to third-party cloud services.
- **Cost-Effective:** Eliminates subscription fees associated with services like ChatGPT Plus or Cloud APIs.
- **Performance Control:** The model's performance depends on your computer's resources, allowing for tailored usage based on your hardware capabilities.

---

#### **4. Installing and Setting Up AMA**

**Step 1: Download AMA**

- Visit the AMA official website (Note: Replace with the actual URL).
- Download the version compatible with your operating system (Windows, macOS, Linux).

**Step 2: Install AMA**

- Follow the installation instructions provided on the website.
- Ensure that AMA commands are accessible via the terminal after installation.

**Step 3: Open Terminal**

- Launch your terminal application to execute AMA commands.

---

#### **5. AMA Command-Line Usage**

AMA requires basic knowledge of terminal commands. Below are the essential commands for setting up AMA with Obsidian:

- **List Available Commands:**

    ```
    lama
    ```

    This command displays all available AMA commands. The primary commands needed are:

    - `pull`: Download models.
    - `list`: List downloaded models.
    - `run`: Run a model in the terminal.
    - `serve`: Start a local server for Obsidian integration.

---

**Command 1: Download a Model**

- **Syntax:**

    ```
    lama pull <model-name>
    ```

- **Example:**

    ```
    lama pull llama3
    ```

    This command downloads the specified model (e.g., `llama3`) if it's not already present on your machine.

- **Verify Downloaded Models:**

    ```
    lama list
    ```

    This command lists all models currently downloaded on your machine.

**Command 2: Run a Model in Terminal**

- **Syntax:**

    ```
    lama run <model-name>
    ```

- **Example:**

    ```
    lama run llama3
    ```

    This command starts a chat session with the specified model directly in the terminal, allowing you to interact with the AI.

**Command 3: Start a Local Server for Obsidian**

- **Syntax:**

    ```
    lama serve --origin "app://obsidian.md" <model-name>
    ```

- **Example:**

    ```
    lama serve --origin "app://obsidian.md" llama3
    ```

    This command starts a local server that Obsidian can interact with, enabling AI functionalities within the Obsidian app.

    > **Note:** To avoid CORS (Cross-Origin Resource Sharing) issues, it's essential to specify the origin as shown above.

    **Pro Tip:** The presenter mentions that the exact command will be provided in the video description for easy copying and pasting.

---

#### **6. Configuring Obsidian to Use AMA**

**Step 1: Open Obsidian and Navigate to Copilot Plugin Settings**

- Open your Obsidian application.
- Access the Copilot plugin settings.

**Step 2: Change the Default Model to AMA Local**

- In the Copilot settings, locate the option to select the AI model.
- Change the default model from the previously used cloud-based model to `AMA Local`.

**Step 3: Specify the AMA Model**

- Scroll down to the `AMA Model` section.
- Specify the model you wish to use (e.g., `llama3`).

**Step 4: Save and Reload Configuration**

- After selecting the desired model, save the settings.
- Reload the Obsidian configuration to apply the changes.

> **Important:** Ensure that you choose a model that matches your machine's resource capabilities to prevent performance issues.

---

#### **7. Recommendations and Considerations**

- **Hardware Requirements:** Running larger models like LLaMA 3 may require significant RAM and processing power. Users with limited resources may experience slow performance or system freezes.
    - **Recommendation:** For machines with smaller RAM (e.g., 8GB), opt for smaller models like `F3` for smoother operation.
- **Data Privacy vs. Performance:** While local models enhance data privacy, they may not match the speed and responsiveness of cloud-based services. Users need to balance privacy with performance based on their specific needs and hardware capabilities.

---

#### **8. Conclusion**

By integrating AMA with Obsidian, users can leverage powerful AI tools for their note-taking and productivity without compromising data privacy. AMA simplifies the process of running local LLMs, making advanced AI functionalities accessible even to those with limited technical expertise.

---

#### **9. Additional Resources**

- **Video Reference:** For a visual guide, the presenter recommends watching another video that demonstrates using AMA with Obsidian for various AI tasks like summarization, translation, template creation, etc.
- **Subscribe for More:** The presenter encourages viewers to subscribe to the channel for more tutorials and insights on utilizing AI for productivity while maintaining data privacy.

---

### **Summary of Commands and Code Snippets**

Below is a consolidated list of the terminal commands mentioned in the video for easy reference:

```
# Display available AMA commands
lama  
# Download a specific model (e.g., llama3)
lama pull llama3  
# List all downloaded models
lama list  
# Run a specific model in the terminal (e.g., llama3)
lama run llama3  
# Start a local server for Obsidian with a specific model (e.g., llama3)
lama serve --origin "app://obsidian.md" llama3
```

**Obsidian Copilot Configuration Steps:**

1. Open Obsidian and navigate to Copilot plugin settings.
2. Change the default model to `AMA Local`.
3. Scroll to the `AMA Model` section and specify your chosen model (e.g., `llama3`).
4. Save the settings and reload the configuration to apply changes.

[[Obsidian]] [[LLM]]  [[AMA + LangChain.js for RAG]]
