---
tags:
- editors
---

## **AER Coding for Free

### Overview

The video introduces **AER**—a tool that works seamlessly with popular generative AI tools such as **ChatGPT** and **Claude**. The focus is on utilizing these AI services in combination with AER to apply code edits directly to files, streamlining the workflow and avoiding the need for direct code writing. This approach is particularly appealing because it allows users to leverage free-tier access to AI tools for coding tasks.

### How-To Instructions

1. **Upgrading or Installing AER**

    - Run the following command to upgrade AER to the latest version or install it if you're new:

        ```bash
        pip install --upgrade aer
        ```

    - If you don’t have AER, running the above command will install it.

2. **Configuring AER for Copy and Paste Use**

    - AER requires an AI model to apply code changes. The video recommends using **Gemini Flash** because it’s fast, has a good rate limit, and is **free**.
    - To use Gemini Flash:
        - Visit **Google AI Studio** to get the API key.
        - Add the environment variable in the terminal:

            ```bash
            export AER_MODEL_API_KEY=<Your_Gemini_Flash_API_Key>
            ```

    - If you want to set Gemini as the default model:

        ```bash
        export AER_MODEL=gemini
        ```

    - Alternatively, you can add these variables to an environment file (`.env`) in the working directory, and AER will automatically load them.

3. **Generating Code Using Chat Interfaces**

    - Choose a chat interface (e.g., **ChatGPT**, **Deep Seek**, or **Claude**) to generate the code you want to use.
    - Example: Generate a simple to-do app using HTML, CSS, and JavaScript.
    - Copy the generated code from the chat.

4. **Applying Clipboard Code Edits Using AER**

    - Run AER with the `apply` flag to use the code in your clipboard:

        ```bash
        aer apply --clipboard <file_name>
        ```

    - If `<file_name>` does not exist, AER will create it and insert the code.
    - Example:

        ```bash
        aer apply --clipboard todo.html
        ```

    - The code is then applied to the file, and you can test the output immediately.

5. **Editing Existing Code**

    - If you want to make changes, ask your preferred chat interface (e.g., ChatGPT) to modify the code (e.g., add an "Edit" button to the to-do app).
    - Copy the new code and run the same AER command to apply the edit.

6. **Working with Larger Codebases**

    - When working with a larger repository or multiple files, use the **Files to Prompt** tool:
        - This tool concatenates all files in a directory into a single prompt to give the full context to the language model.
        - Example command:

            ```bash
            aer files-to-prompt <directory_path>
            ```

        - The output will be a single prompt containing all the context needed.
        - After providing the context, request changes from your chosen chat interface.
        - Copy each file change individually and apply them using AER, one file at a time.

7. **Tips for Applying Changes Across Multiple Files**

    - When dealing with changes that span multiple files:
        - Apply the changes for each file one by one.
        - It may be a bit tedious, but it ensures you maintain control and accuracy, especially when working for **free** without sacrificing code quality.

### Key Ways to Use These Tools for Free

- **Generative AI Services**:
    - Use **ChatGPT** (free tier) or **Deep Seek** to generate code. These tools are less rate-limited compared to other services like **Claude**, which can be more restrictive.
    - Since AER takes care of code application, you only need the generative AI to provide code suggestions.
- **Gemini Flash Model**:
    - Use **Gemini Flash**, a free model with a good rate limit, to apply code edits via AER.
    - The tool doesn’t require generating new code—just applying changes—so a free-tier model is sufficient.
- **Simple Workflow with Environment Variables**:
    - Setting up the model using environment variables (`AER_MODEL`) makes the setup efficient and doesn’t require any subscription services.
- **Manual Application**:
    - The manual process of applying edits across multiple files allows you to get the best out of free tools without relying on costly integrated solutions.

### Summary

- **AER** is a powerful tool to apply code edits using AI-generated code.
- You can generate code via **ChatGPT**, **Claude**, or other free chat interfaces, and use **Gemini Flash** for applying changes.
- The latest version of AER allows you to work on a larger codebase using the **Files to Prompt** tool.
- By following these steps, you can use these tools efficiently without incurring costs, allowing you to create and maintain quality code.

This approach is particularly suitable for users who want to code without compromising on quality while avoiding expensive AI subscriptions. The use of **Gemini Flash** and environment variable configurations makes the process flexible and accessible.

[[Code Editor]]