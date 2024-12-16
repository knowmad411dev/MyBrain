---
tags:
- editors
- vscode
video-url: https://www.youtube.com/watch?v=myqHyLfTZOY&list=WL&index=2
---

## **Overview of Aider Composer**

Aider Composer is an extension for VS Code that offers a graphical interface to control Aider, making it more accessible for users who prefer a GUI instead of a terminal interface. It is comparable to Cursor's Composer but uses Aider as a backend, which retains the power and efficiency of Aider while making it more user-friendly.

**Features of Aider Composer**

1. **Graphical Interface**: Unlike traditional Aider, which runs through a terminal, Aider Composer integrates directly into VSCode with a graphical interface, making it accessible to more users.
2. **All Modes Supported**: It supports various chat modes similar to the original Aider, allowing users to edit code, review changes, or simply ask questions.
3. **Review Code Changes**: Users can review and approve code changes before they are applied, making it easier to maintain control over modifications.
4. **Chat History**: Aider Composer saves chat sessions, allowing you to refer back to past interactions, similar to other tools like Cursor's Composer.
5. **File Management**: Users can easily add, remove files, and toggle between read-only and editable modes with just a click.
6. **Integrated with VS Code**: Users can reference files in VS Code and manage them using Aider Composer's GUI interface, adding to its efficiency.
7. **Uses Installed Aider Backend**: Instead of creating its own version of Aider, Aider Composer uses the existing Aider installation on your computer, which ensures that it remains lightweight and efficient.

**Limitations**

1. **No Multiple Workspace Support**: Aider Composer currently does not support multiple workspaces.
2. **Limited Git and Linting Features**: Features such as Git integration, linting, testing, voice commands, and inline commands are currently not available, though these may be added in future updates.
3. **Setup Complexity**: Setting up Aider Composer can be challenging, especially for non-Windows users, due to specific requirements for the Python executable path.

**How to Set Up Aider Composer in VS Code**

1. **Install Aider Composer Extension**:
   - Open VS Code.
   - Go to Extensions and search for "Aider Composer" and install it.

2. **Set Python Path for the Extension**:
   - After installing the extension, navigate to VS Code settings.
   - Search for "Composer" settings.
   - Set the Python executable path for Aider Composer to use.

3. **Setting Up a Python Virtual Environment**:
   - Create a virtual environment by running the following commands:
     ```bash
     python -m venv <environment_name>
     ```
   - Activate the virtual environment:
     - On Windows:
       ```bash
       .\<environment_name>\Scripts\activate
       ```
     - On Unix/macOS:
       ```bash
       source <environment_name>/bin/activate
       ```
   - Install Aider and Flask in the virtual environment:
     ```bash
     pip install aider flask
     ```
   - Run `pwd` to get the path of the virtual environment and add `/bin` to it.
   - Set this path in the VS Code settings under the Aider Composer Python path.

4. **Windows-Specific Setup**:
   - Install Python 3.10 and make sure to check the "Add to PATH" option.
   - Open a terminal and install Aider and Flask using the following command:
     ```bash
     pip install aider flask
     ```
   - Set the environment variables by copying the Python path and adding it to the VS Code settings under the Aider Composer Python path.

5. **Configure Provider**:
   - Configure the Aider Composer extension with the provider you wish to use. Supported options include OpenAI, Anthropic, or any OpenAI-compatible API.
   - Enter the base URL, model name, and API credentials in the settings as per the chosen provider.

**Using Aider Composer**

- **Sidebar Features**:
  - Once installed, Aider Composer appears in the sidebar in VS Code.
  - The **Settings** option allows you to change providers.
  - The **History** option lets you view past sessions.
  - Use the **Add** button to create a new session.
- **Working Modes**:
  - **Ask Mode**: This mode only reads files and does not make modifications.
  - **Code Mode**: This mode allows Aider Composer to write and edit files.
  - **File Specific Edits**: You can specify particular files to edit, similar to Cursor Composer, for more targeted changes.
- **Reviewing Changes**:
  - In **Code Mode**, you can ask Aider Composer to make modifications, e.g., generating a simple game using HTML, CSS, and JavaScript.
  - Once Aider Composer has generated code, you can review the changes in VS Code. You can approve or reject the changes using a tick icon at the top.

**Example**: Creating a Simple Game
- Switch to **Code Mode**.
- Enter a prompt like: "Create a Minesweeper game using HTML, CSS, and JavaScript."
- Aider Composer generates the game files.
- Review the generated files and use the tick icon to approve them.

**Summary**

Aider Composer is a powerful and accessible way to leverage Aider's capabilities directly within VS Code without needing to work through a terminal interface. It simplifies code changes, provides a user-friendly GUI, and allows users to easily manage their workflow with approval processes and chat history, making it ideal for anyone looking to integrate AI-based assistance into their coding environment.

[[VSCode]]  [[Code Editor]]