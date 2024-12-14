---
tags:
- gpt
- vscode
- editors
video-url: https://www.youtube.com/watch?v=cVBi-wuA7u8&list=WL&index=2
---
## **ChatGPT in Visual Studio Code

**Overview of Setting Up CodeGPT in VS Code**

This guide will help you set up and use CodeGPT, an AI coding assistant, within Visual Studio Code (VS Code). We'll walk through each step, including the required extensions, installation process, API integration, and how to start using CodeGPT for your coding needs. Here, you'll find how-to instructions, key code examples, and some practical tips to get started.

### **Prerequisites**

- **VS Code**: Make sure you have Visual Studio Code (VS Code) installed. You can download it from the official [Visual Studio Code website](https://code.visualstudio.com/). VS Code is available for Windows, macOS, and Linux, and is a free, open-source code editor that supports various programming languages and extensions.

### **Step-by-Step Installation Guide**

1. **Open VS Code**
   - Once installed, open VS Code on your computer.

2. **Install the CodeGPT Extension**
   - On the left sidebar of VS Code, locate and click the **Extensions** icon (which looks like four small boxes with one floating away).
   - In the search bar, type **"CodeGPT"**. You will see multiple results.
   - Look for the extension with the **blue icon** labeled "CodeGPT: Chat & AI Agents" and click **Install**.

3. **Activate the Extension**
   - After installing the CodeGPT extension, an **icon will appear** on the left-hand sidebar in VS Code. Click on this icon.
   - At the top of the CodeGPT sidebar, you will see a **drop-down menu** labeled **"Select your AI"**.

4. **Select OpenAI as the LLM Provider**
   - By default, CodeGPT might be set to use its own AI model, but you can switch to other providers.
   - In the drop-down menu, navigate to **"Third Party"** and select **"OpenAI"**.

5. **Configure Model Selection**
   - CodeGPT allows you to use **OpenAI GPT-3.5** or earlier models for free. However, for optimal results, select **GPT-4** (also known as "40").
   - The GPT-4 model offers significantly improved performance compared to earlier versions.
   - Click **Connect** after selecting the desired model.

6. **Generate and Connect an OpenAI API Key**
   - To use CodeGPT with OpenAI, you will need an **API key**.
   - Go to [OpenAI's Platform](https://platform.openai.com) to **create an account** if you don't already have one.
     - You can **sign in with Google** to make the process quicker.
   - After signing up, OpenAI will prompt you for account details and request verification via your phone number.
   - Once verified, go to **API Key Management** and click **Create Secret Key**.
   - A unique **API key** will be generated — click **Copy** to copy the key to your clipboard.
   - Return to VS Code, paste the **API key** in the CodeGPT configuration panel to connect VS Code to your OpenAI account.

### **Upgrading to GPT-4 (Optional)**

- If you want to use GPT-4, which generally provides better results, you will need to **purchase credits**.
- In VS Code, if you try to use GPT-4 without upgrading, you'll get a message that says **"you don’t have access to the model."**
  - Click **Increase Limit** and follow the steps.
- OpenAI offers a **free tier**, but to use GPT-4, you need to switch to a **paid account**.
- Upgrading costs only **pennies per query** for small projects.
  - You can set a budget, such as adding **$5 of credit**, which is often more than enough to start.
  - During payment, you can unselect the **"Automatically recharge my card"** option so that you control how much is charged.

### **Testing the Connection**

- Now that you have your API key entered and your credits set up, you can **ask CodeGPT if it’s ready to work**.
- Enter a simple command like "**Are you ready to work?**" to verify. If the extension replies with "**I am connected**" and mentions available credits, you're good to go.

### **Using CodeGPT to Insert Code**

- With CodeGPT connected, you can begin **prompting it for code examples or troubleshooting help**.
- Enter your requirements in the chat box, and the model will generate the appropriate code for you.
- You can **insert the generated code directly** into your file by clicking the **Insert** button located next to the code snippet provided.
- Example: You could prompt CodeGPT with "**Create a simple Python function that reads a text file and prints each line**," and CodeGPT will generate the code block for you.

### **Practical Tips for Using CodeGPT**

- **Language Support**: CodeGPT works for many programming languages such as **JavaScript, Python, HTML/CSS**, etc. Just specify the language in your prompt if needed.
- **Project Integration**: You can use CodeGPT to **refactor existing code** by copying parts of your code into the prompt and asking for improvements or bug fixes.
- **Code Insertion**: Once the extension generates code, you can choose to insert it **at the top or any specific location** within your current file.

### **Cost Management**

- OpenAI's API charges are minimal, especially for **small projects**. Costs are calculated per token (where a token can be as little as one character), so **$5 of credits** can last a long time unless you're making a huge number of complex requests.
- By disabling the **"automatic recharge"** option, you maintain full control over your spending.

### **Conclusion**

Setting up CodeGPT in VS Code enables you to leverage powerful AI coding assistance directly within your development environment. By following these steps to install the extension, connect an OpenAI API key, and manage your usage, you'll have a seamless experience that can greatly speed up coding tasks, improve productivity, and help you solve coding challenges quickly.

If you follow the setup instructions above, you can start asking CodeGPT to help with generating code, debugging, and even explaining complex functions—all from within VS Code.

[[ChatGPT]]   [[VSCode]]  [[GPT]]  [[Code Editor]] 
