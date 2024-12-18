---
tags:
- vscode
- editors
---
## **Detailed Overview: Visual Studio Code Setup with Gemini Models and CoPilot Arena**

This guide will walk you through setting up a **free coding assistant** in Visual Studio Code using the latest Gemini models and CoPilot Arena. By combining these tools, you can get high-quality code suggestions without paying for premium APIs like GPT-4 or Claude 3.5.

---

### **1. Tools and Extensions You Will Use**

- **CoPilot Arena**: Free AI-powered code completion.
- **Cline Extension** (previously Claudia): Connects genetic models (like Gemini).
- **Google Gemini Models**: Free, high-quality models for code generation.
- **AI Studio**: Source for obtaining your API key.

---

### **2. Installing CoPilot Arena**

1. Open Visual Studio Code.
2. Go to the **Extensions Tab**.
3. Search for **CoPilot Arena** (even if you type it slightly wrong, it should show up).
4. Install the extension.

Once installed, CoPilot Arena will appear in the sidebar as a **two-swords icon**.

---

### **3. Setting Up CoPilot Arena**

- CoPilot Arena provides access to models such as:
    - GPT-4
    - Claude Sonnet 3.5
    - Google Gemini 1.5 Pro
    - Gemini 2 Flash (faster, lightweight model)
- It also allows you to rank models and create a **leaderboard** for preferences.

#### **Key Features**:

- It generates **two suggestions** for you to choose from.
- Models are free to use and easy to switch between.

---

### **4. Installing and Configuring Cline**

1. Go to the **Extensions Tab**.
2. Search for **Cline**.
3. Install the extension.

**Cline** works with genetic models, particularly the Gemini 2 Flash and Gemini 126 Experiment, which are powerful and free to use.

---

### **5. Configuring the AI Providers**

#### **First Model Setup (Gemini 2 Flash):**

1. Go to [AI Studio](https://ai.google.com/studio).
2. Obtain your **AI Key**.
3. In Cline settings, select **Google Gemini** as your AI provider.
4. Paste the AI Key.
5. Select the model: **Zite 2 Flash Experiment**.
6. Click **Done**.

#### **Second Model Setup (Gemini 126 Experiment):**

- Use OpenAI-compatible settings to connect the model.
- Enter the **Base URL** and **Model ID** provided below:
    - **Base URL**: _Your-Base-URL_
    - **Model ID**: _Gemini Experiment 126_.
- Paste your API key and complete the setup.

---

### **6. Using Gemini Models for Code Generation**

1. Open your project.
2. Use CoPilot Arena or Cline to request code completions:
    - CoPilot Arena provides **two suggestions**.
    - Cline auto-completes based on the active model.
3. Switch between models (Gemini 2 Flash for speed, Gemini 126 for quality).

**Example**:

- If coding a **Next.js e-commerce page** with Tailwind CSS:
    - Start with **Cline**.
    - Input a prompt: "Create a modern e-commerce page with Tailwind and dark mode."
    - Use prompt enhancement for better results.

#### **Prompt Enhancement**:

- Tools like **bolt.new** help enhance your prompt automatically.
- Example:
    
    ```
    Create a modern minimalist e-commerce website with:
    - Hero section
    - Product grid
    - Tailwind CSS dark mode
    - Responsive design
    - GSX structure with proper components and CSS classes.
    ```
    

Copy the enhanced prompt into Cline to improve code quality.

---

### **7. Prompt Enhancement Tips**

1. **Be specific** with details:
    - Layout, colors, and structure requirements.
2. Use **Zero-Shot Chain of Thought**:
    - Add "Step by Step" to your prompts to improve reasoning.
3. Paste project folders into Cline for context:
    - Use **Add Folder** or **Add Files** options in Cline.

**Example Prompt**: "Create a responsive product page using the app router and Tailwind CSS with images, hover effects, and a grid layout. Add a review section, product details, and a navbar."

---

### **8. Dealing with Rate Limits**

- **Error 429**: Occurs when hitting free-tier limits.
- **Solution**:
    - Wait a few seconds.
    - Retry the request.
- Gemini 2 Flash has better rate limits compared to the 126 Experiment model.

---

### **9. Code Completion in Action**

- Example Setup:
    
    ```javascript
    export async function getProducts() {
        return new Response(JSON.stringify({ products: [] }));
    }
    ```
    
- CoPilot Arena will suggest auto-completions when you type.
- Choose the best suggestion by pressing **Tab**.

#### **Inline Editing**:

1. Highlight code.
2. Press **Ctrl + I** to request an inline improvement.
3. Select between suggestions using **Ctrl + 1** or **Ctrl + 2**.

---

### **10. Advanced Custom Instructions**

- Add custom instructions in Cline settings for improved performance.
- Example (from Reddit):
    
    ```
    You are a coding assistant that writes clean, optimized, and modular code. Follow best practices for responsive design and modern UI development.
    ```
    

Paste this into the **Custom Instructions** box in Cline for the model you use.

---

### **11. Summary of Model Performance**

- **Gemini 126 Experiment**: High-quality code but strict rate limits.
- **Gemini 2 Flash**: Faster with more flexible rate limits.
- **Claude Sonnet 3.5**: Benchmark model, but requires payment.

**Recommendation**: Use both models to balance speed and quality.

---

### **12. Conclusion**

This setup is ideal for developers who need free, high-quality code suggestions. By combining Gemini models with CoPilot Arena and Cline, you can:

- Generate clean and structured code.
- Improve productivity without paid APIs.
- Balance speed (Flash) and quality (126 Experiment).

**Tip**: Enhance prompts, switch models as needed, and use inline editing for best results.

---

### **Links and Resources**

- **CoPilot Arena Extension**: [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/)
- **Cline Extension**: [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/)
- **AI Studio for Gemini API Keys**: [AI Studio](https://ai.google.com/studio)
- **Bolt.new**: [bolt.new](https://bolt.new/)

[[Code Editor]]   [[VSCode]]  