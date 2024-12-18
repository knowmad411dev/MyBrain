---
tags:
- vscode
- editors
---
## **Copilot Arena with Vscode

**Detailed Overview of Two Free Visual Studio Code Tools**

---

### **1. Copilot Arena**

#### **Overview**

Copilot Arena is a free code completion extension for Visual Studio Code. It allows you to use multiple AI models like **GPT-4.0**, **Codex**, **LLaMA 3.1**, **Quinn**, and **Sonnet 3.5** for autocomplete within the editor. It is considered superior to other tools like _SuperMove_ and _Continue_.

#### **Installation Instructions**

1. Open **Visual Studio Code**.
2. Go to the **Extensions** tab (Ctrl+Shift+X).
3. Search for **"Copilot Arena"**.
4. Click **Install** to add the extension.

#### **Important Settings**

By default, Copilot Arena may collect your code for training purposes. To ensure privacy:

1. Go to the **Extensions** tab.
2. Search for **"Copilot Arena"**.
3. Click the **Manage** button (gear icon) and select **Settings**.
4. In the settings window:
    - Change the "Research" option to **Private**.
    - This ensures no code is uploaded for training, though code will still be sent to the AI provider for completion.

#### **Usage Instructions**

1. Start typing your code. For example:
    
    ```javascript
    export async function getShorterOrders() {
    ```
    
2. Copilot Arena will suggest autocompletions.
    - Example: It may generate two variations of the function based on the AI models used.
3. To accept a suggestion:
    - Press **Tab** to accept the first suggestion.
    - Use the following shortcuts for alternatives:
        - **Ctrl+1**: Accept the first option.
        - **Ctrl+2**: Accept the second option.
        - **Ctrl+N**: Reject the suggestion.

#### **Prompt Enhancement**

You can also enhance prompts within the editor:

1. Highlight a piece of code.
2. Press **Ctrl+I** (or Command+I on macOS).
3. This opens a prompt box where you can add instructions.
    - Example: "Give an error if the ID of the order is not provided."
4. Copilot Arena generates multiple code options based on your instructions. Accept the preferred option.

**Example:**

- AI-Generated If Statement:
    
    ```javascript
    if (!id) {
        throw new Error("ID is required");
    }
    ```
    

#### **Model Selection and Feedback**

- Copilot Arena shows the models used (e.g., _Claude 3.5_, _Sonnet_) and indicates which models performed better.
- You can register to maintain a list of favorite models, though registration is not required.

#### **Advantages**

- Free access to powerful autocomplete.
- Real-time comparison between AI model outputs.
- Simple toggle between suggestions using keyboard shortcuts.

---

### **2. AI Toolkit by Microsoft**

#### **Overview**

The AI Toolkit is an official extension by **Microsoft** for integrating AI models directly within Visual Studio Code. It supports models hosted by GitHub, Google, Anthropic, OpenAI, and other providers.

#### **Installation Instructions**

1. Open **Visual Studio Code**.
2. Go to the **Extensions** tab (Ctrl+Shift+X).
3. Search for **"AI Toolkit"**.
4. Click **Install** to add the extension.

#### **Accessing the AI Toolkit**

1. After installation, go to the **Welcome Page** of Visual Studio Code.
2. Click on **"Explore AI Models"**.
3. Select the models based on the following filters:
    - **Hosted by:** GitHub, OpenAI, Google, etc.
    - **Task Type:** Code completion, generation, etc.
    - **Device Type:** Local or Remote.

#### **Free GPT-4.0 Access**

You can access **GPT-4.0 for free** directly through GitHub's hosting:

1. Select **GPT-4.0** in the model catalog.
2. Open the AI Playground.
3. Add your **System Prompt**. Example:
    
    ```
    Design a visually appealing homepage for an airline website using Tailwind CSS.
    The page should focus on enabling users to book tickets online.
    ```
    
4. The AI generates relevant code examples.

#### **Using the Generated Code**

- Copy the generated code and paste it into your desired file within Visual Studio Code.

**Example Output:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Airline Booking Website</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body>
    <div class="container mx-auto text-center">
        <h1 class="text-4xl font-bold mt-8">Welcome to Airline Booking</h1>
        <button class="bg-blue-500 hover:bg-blue-700 text-white py-2 px-4 mt-4">
            Book Tickets
        </button>
    </div>
</body>
</html>
```

#### **Testing Other Models**

- AI Toolkit supports other models such as **LLaMA**, **Claude**, and **Cohere**.
- Some models may require API keys (e.g., Anthropic's Sonnet 3.5).

#### **Notable Models Accessible for Free**

- **GPT-4.0**: Hosted via GitHub.
- **LLaMA Models**.
- **Google's Free AI API**.

#### **Advantages**

- Direct access to multiple AI models.
- Playground to test prompts without switching tabs.
- Supports system prompts and interactive coding.

---

### **Final Thoughts**

Both **Copilot Arena** and **AI Toolkit** are exceptional tools for Visual Studio Code that enable advanced AI-based code suggestions and generation **for free**.

- **Copilot Arena** is perfect for **real-time code completion** with multiple AI models.
- **AI Toolkit** serves as a central hub for exploring and using different models, including free GPT-4.0 access.

These tools reduce friction in switching tabs or screens, making coding workflows smoother and faster. You can now integrate AI-powered coding assistants seamlessly into your development environment without spending a dime.

---

**Key Shortcuts Recap**

|Action|Copilot Arena Shortcut|
|---|---|
|Accept First Suggestion|Tab|
|Accept First Result|Ctrl+1|
|Accept Second Result|Ctrl+2|
|Reject Suggestion|Ctrl+N|
|Enhance Prompt|Ctrl+I|

[[VSCode]]  [[Code Editor]]  