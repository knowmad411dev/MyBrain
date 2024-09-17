# Start Your "Personal AI Ecosystem": Fabric Client Mac Installation
https://www.youtube.com/watch?v=LyyvVVsAPsk

![](https://www.youtube.com/watch?v=LyyvVVsAPsk)
## Summary:

**Summary: Setting Up Fabric AI with Visual Studio Code**

The video describes the speaker’s journey to successfully setting up and using Fabric AI, particularly aimed at non-coders who want to integrate AI into their workflows. It provides step-by-step instructions for installing the necessary tools, configuring Fabric AI, and creating an essay using AI patterns. The speaker emphasizes learning through trial and error and highlights the capabilities of Fabric AI.

### Key Information:

- **Introduction**:
    
    - The speaker, a non-coder, explains how they made a breakthrough using Fabric AI and provides a step-by-step guide for others to follow.
    - The focus is on helping people integrate AI into their work without deep technical knowledge.
- **Background and Motivation**:
    
    - Inspired by Daniel Miessler's blog post and his philosophy that AI enhances human creativity.
    - Fabric AI ecosystem can augment productivity by simplifying tasks like summarizing, writing essays, and more.
- **Step-by-Step Instructions**:
    
    1. **Install Visual Studio Code (VS Code)**:
        
        - Download and install VS Code as an Integrated Development Environment (IDE).
    2. **Get an OpenAI API Key**:
        
        - Obtain an API key from OpenAI, as it is required for connecting AI functionality within Fabric AI.
    3. **Download Fabric AI Source Code**:
        
        - Access Daniel Miessler’s GitLab repository for the Fabric AI source code.
        - Download the zip file (93 MB) and extract it to a specific folder.
    4. **Open Fabric in Visual Studio Code**:
        
        - In VS Code, open the extracted folder using the "Open" button.
        - Navigate to the "fabric_main" folder and open the client directory in the terminal.
    5. **Install Poetry for Package Management**:
        
        - Use the terminal to install Poetry (`poetry install`), which is essential for managing dependencies.
        - If Poetry fails to install, troubleshoot using Python version commands (`python 3.12`).
    6. **Configure System Settings**:
        
        - Customize the settings file (e.g., `bashrc` for Windows or `zshrc` for Mac) to fit your system requirements.
        - Execute Python scripts using the appropriate commands.
    7. **Create API Key File**:
        
        - Create a new file under the “fabric_main” directory to store the OpenAI API key.
        - Insert the API key and save the file.
    8. **Activate the Fabric AI Help Menu**:
        
        - After the setup, verify the installation by running the command that displays Fabric’s help menu.
- **Using Fabric AI to Write an Essay**:
    
    - Fabric AI offers various patterns for tasks, including writing essays.
    - The speaker demonstrates using a pattern to write an essay about why "Cybersecurity GRC is underrated" by running a command in VS Code.
    - The AI-generated essay was successfully created, showcasing the tool's utility.
- **Key Takeaways**:
    
    - The breakthrough is not just the essay generation but the successful setup and usage of Fabric AI.
    - Fabric AI allows for more sophisticated pattern chaining compared to traditional AI tools like ChatGPT or Bard.
    - The speaker expresses newfound respect for software development, acknowledging the challenges in getting everything set up.
- **Final Thoughts**:
    
    - The process involved significant trial and error, but the speaker hopes to encourage others to break through and achieve success using Fabric AI.
    - The speaker plans to continue exploring the tool's full potential and invites feedback from viewers.

### Step-by-Step Instructions for Setting Up Fabric AI:

1. **Install Visual Studio Code (VS Code)**:
    
    - Download and install Visual Studio Code (VS Code) as an Integrated Development Environment (IDE) from the official website.
    - Follow the on-screen instructions to complete the installation.
2. **Get an OpenAI API Key**:
    
    - Visit the OpenAI website and sign up for an API key.
    - Save the API key, as it will be needed later for connecting Fabric AI to OpenAI.
3. **Download Fabric AI Source Code**:
    
    - Go to Daniel Miessler’s GitLab repository for Fabric AI.
    - Download the source code as a zip file (93 MB).
    - Extract the zip file to a folder of your choice.
4. **Open Fabric AI in Visual Studio Code**:
    
    - Launch Visual Studio Code.
    - Open the extracted Fabric folder by clicking on "File" > "Open Folder" and selecting the directory where you saved the source code.
    - Ensure that the "fabric_main" folder is visible in VS Code.
5. **Open Terminal in Visual Studio Code**:
    
    - In Visual Studio Code, open a new terminal by selecting **Terminal** > **New Terminal**.
    - Navigate to the "client_main" directory by running the command `cd client`.
6. **Install Poetry for Package Management**:
    
    - In the terminal, run the command `poetry install` to install the necessary dependencies for Fabric AI.
    - If Poetry fails to install, troubleshoot using specific Python version commands, such as `python 3.12`.
7. **Configure System Settings**:
    
    - Customize system settings to fit your machine. For example:
        - For Windows, update the `bashrc` file.
        - For Mac, update the `zshrc` file.
    - Copy and paste the required commands from the GitLab documentation into these configuration files.
8. **Create and Insert OpenAI API Key**:
    
    - In the Fabric AI folder, create a new file under the “fabric_main” directory to store the OpenAI API key (e.g., `.env` file).
    - Insert the API key you obtained from OpenAI into this file and save it.
9. **Run Fabric AI Help Menu**:
    
    - In the terminal, run the command to display the help menu for Fabric AI to verify that everything is working correctly.

### Step-by-Step Instructions for Using Fabric AI:

1. **Write an Essay Using Fabric AI**:
    - Open the terminal in Visual Studio Code.
    - Run the command to activate a pattern, such as `write an essay`, from the available Fabric AI patterns.
    - For example, you could run a command like `write me three paragraphs on why Cybersecurity GRC is awesome and underrated`.
    - The AI will generate an essay based on the input and pattern you selected.

By following these steps, you can set up Fabric AI and use it to generate content within Visual Studio Code.

Here is a list of resources mentioned in the video along with associated links (where applicable):

### 1. **Visual Studio Code (VS Code)**:

- The Integrated Development Environment (IDE) used to run Fabric AI.
- [Visual Studio Code Official Website](https://code.visualstudio.com/)

### 2. **OpenAI API Key**:

- The API key is required to connect Fabric AI with OpenAI’s language models.
- [OpenAI API Key](https://platform.openai.com/)

### 3. **Daniel Miessler’s GitLab Repository for Fabric AI**:

- The source code for Fabric AI can be downloaded from this GitLab repository.
- [Fabric AI GitLab Repository](https://gitlab.com/danielmiessler/fabric)

### 4. **Poetry (Python Dependency Management Tool)**:

- Poetry is used to manage dependencies for Fabric AI.
- [Poetry Official Website](https://python-poetry.org/)

### 5. **GitHub (Error Troubleshooting)**:

- GitHub is referenced as a platform for customizing system paths and troubleshooting errors related to Fabric AI setup.
- No specific link provided, but useful for searching for relevant issues.

These resources are essential for setting up and using Fabric AI within Visual Studio Code as demonstrated in the video.


