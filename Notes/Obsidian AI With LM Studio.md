---
github_link: https://github.com/SystemSculpt
tags:
- obsidian
- llm
video-url: https://www.youtube.com/watch?v=zS9FTikQg5c&list=WL&index=16
---

## **Setup Obsidian AI With LM Studio

### Overview of the Content

The text is a tutorial that continues from a previous setup, focusing on testing multiple local Large Language Models (LLMs) integrated with Obsidian. The discussion covers model setup, configurations, and usage with Obsidian’s Text Generator plugin. The tutorial also hints at setting up Python automation for batch processing the model’s responses.

### **Step-by-Step Instructions and How-To Guide:**

#### **1. Loading and Configuring Stable LM2 Model:**

- **Model Information:**
  - Testing the **Stable LM2** model with **1.7 billion parameters**.
  - Model uses the **Zephyr preset structure**.
- **Configuration Instructions:**
  1. **Select the Zephyr Preset** in the local inference server interface.
  2. Set the token length to **4096**, the maximum length for Stable LM2.
  3. **Reload** the model after changing settings.

#### **2. Starting the Local Inference Server:**

- Navigate to the **Local Inference Server** interface.
- Select **Stable LM2** and click to load.
- Set a **Port** for the local inference server (e.g., **1234** in this case).
  - Ensure the port is unused.
- Click to **start the server**.

  > Note: Ignore console details unless developing an external interface.

#### **3. Copying the Local Inference Server URL:**

- Once the server is up, three URLs will be displayed.
  - Copy the **middle URL** using `Cmd + C` (Mac) or `Ctrl + C` (Windows).

#### **4. Setting Up in Obsidian:**

- **Access Obsidian Settings:**
  1. Press `Cmd + ,` (Mac) or `Ctrl + ,` (Windows) to open settings.
  2. Navigate to **Community Plugins** > **Browse**.
  3. Search for **"Text Generator"** and install it.
  4. Avoid updating the plugin if there are recent breaking changes.

- **Configuring Text Generator Plugin:**
  1. In the settings, click **Text Generator** > **LLM Provider Settings**.
  2. Select **"Custom"** as the provider.
  3. Remove anything in the **Endpoint** field and paste the copied URL (`Cmd + V` or `Ctrl + V`).
  4. In the **Headers section**, under **Authorization**, type `"Bearer not needed"`.
  5. All code snippets or settings should ideally auto-populate.

#### **5. Additional Settings and Configurations:**

- **Enable Modal and Modal Suggest:**
  1. Click **Text Generator** in the plugin settings.
  2. Type **"modal"** and enable both **modal** and **modal suggest** options.

- **Script Setup for Testing:**
  1. Navigate to **GitHub** to download the necessary script for testing (`gen_relations.md`).
  2. Click **Copy Raw File** to copy the raw code to your clipboard.
  3. In **Obsidian**, go to **Advanced Settings**.
  4. Set the **Prompt Templates Path** to the folder where your prompt templates are saved (e.g., `/three/templates/text_generator/prompts`).
  5. Paste the script (`gen_relations.md`) in the specified folder for prompt templates.

#### **6. Running a Simple Text Generation Test:**

- **Generate Text within Obsidian:**
  1. Type a simple question, e.g., **"What is an LLM?"**.
  2. Press `Cmd + P` (Mac) or `Ctrl + P` (Windows) to open the **Command Palette**.
  3. Search for and select **Generate Text** (or use your custom hotkey).
  4. The plugin will show **Processing** and generate a response.

- **Observing Local Inference Server:**
  1. Go to **LM Studio** and observe the local inference server console.
  2. You’ll see logs like:
     - Question received.
     - Streaming responses and tokens.
     - Final completion.
- **Result Verification in Obsidian:**
  1. Return to Obsidian to see the generated answer.
  2. Example response: An LLM (Large Language Model) is an AI that understands and generates human-like text.

#### **7. Python Automation for Testing Models:**

- The author intends to **automate** the testing of all models using a **Python script**:
  - This script will iterate through models, run tests, and save responses to a text file.
  - The saved results will be sent to **GPT-4** for analysis.

  > Note: GPT-4 is mentioned as the **benchmark** for evaluating model performance.

#### **8. Summary of Current Setup:**

- The setup includes:
  - **Local Inference Server** connected to Obsidian via the **Text Generator plugin**.
  - Testing **Stable LM2** to generate answers and verify functionality.
- **Future Goal:**
  - Evaluate multiple models using automation.
  - Compare models for day-to-day tasks and pick the best local LLM for personal use.

#### **9. Next Steps in the Video Series:**

- The tutorial ends by noting that the **testing** will continue in the next video, with a **ranking of the models** in terms of suitability for integration with Obsidian.

---

### **Code and Specific Commands Mentioned:**

1. **Copying URL from Local Inference Server:**
   - **Command:** `Cmd + C` (Mac) or `Ctrl + C` (Windows)

2. **Obsidian Plugin Installation:**
   - Navigate to **Community Plugins**.
   - Search for **Text Generator**.

3. **Custom LLM Provider Setup:**
   - Paste the URL in the **LLM Provider Settings**.
   - Set authorization header: `"Bearer not needed"`.

4. **Running Text Generation:**
   - **Command Palette:** `Cmd + P` or `Ctrl + P`
   - **Command:** **Generate Text**

5. **GitHub Script Setup for Testing:**
   - Navigate to **GitHub**.
   - Download `gen_relations.md` template.
   - Place in prompt templates path.

### **Tips and Observations:**

- **Model Setup & Testing Environment:**
  - Make sure you have sufficient RAM (e.g., 16 GB) to ensure that the model loads properly.
  - Choose an unused port to avoid conflicts.
- **Obsidian Plugin Caution:**
  - Avoid updating the **Text Generator** plugin during active testing, as it might contain breaking changes.
- **Python Automation:**
  - Python scripting is suggested for automating model testing, logging outputs, and comparing results using **GPT-4**.

### **Summary of Key Tools & Links:**

- **Stable LM2** Model - A local LLM with 1.7B parameters.
- **Obsidian** - Note-taking tool, integrating LLM responses for personal notes.
- **Text Generator Plugin** - Plugin to connect Obsidian to custom LLM endpoints.
- **LM Studio** - Used for monitoring local inference server activity.
- **GitHub** - For obtaining prompt templates (`gen_relations.md`) required for testing.

### **Final Remarks:**

- The user successfully completed the setup of their local LLM and was able to generate text within Obsidian.
- The next step will involve comparing models to determine the best fit for their day-to-day productivity needs, using automation for efficient benchmarking.

The tutorial offers a hands-on approach for integrating local LLMs with tools like Obsidian, emphasizing experimentation, flexibility, and leveraging Python scripting for future enhancements.

[[Obsidian]]  [[LLM]]