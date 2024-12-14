---
TAGS:
- vscode
- agents
- editors
github_link: https://github.com/gitdagray
video-url: https://www.youtube.com/watch?v=he0_W5iCv-I&list=WL&index=1
---
## **VS Code AI Coding Assistant with Open Source Models

# Overview

This guide shows you how to set up a **free AI coding assistant** in Visual Studio Code (VS Code) using open-source models to keep your code 100% local. This method provides a cost-effective, privacy-focused alternative to tools like GitHub Copilot, utilizing tools such as **Ollama** (an AI model manager), **CodeQuin** (a code generation model), and **Continue** (a VS Code extension).

The aim is to have a powerful AI assistant fully integrated within VS Code that can deliver results similar to paid services, but for free.

## Prerequisites

1. **VS Code**: Make sure you have Visual Studio Code installed.
2. **Terminal Knowledge**: Understand basic command line operations within VS Code.
3. **Ollama and Continue Extensions**: You'll need these for downloading and running the AI model.

## Step-by-Step Instructions

### Step 1: Download and Install Ollama

- **Navigate to ama.com** and download **Ollama** for your operating system. It’s available for:
  - **Windows (Preview)**
  - **Mac OS**
  - **Linux**
- After downloading, install Ollama. On Windows, you may need to **restart your computer** to ensure the terminal recognizes the command.

### Step 2: Verify Ollama Installation

- Open the VS Code terminal by pressing `Ctrl + \`` (back tick).
- Run the following command:
  ```bash
  ollama del
  ```
- If the command fails, **restart** your computer.

### Step 3: Select a Model from Ollama

- The recommended model is **CodeQuin**, chosen for its relatively small size of **4.2GB** (compared to DeepSeaCoder, which is **8.9GB**).
- Search for **CodeQuin** on the Ollama page and run the command:
  ```bash
  ollama run codeQuin
  ```
- This will download and initialize the model. Note that it may take some time to complete.

### Step 4: Install and Configure the Continue Extension in VS Code

- In VS Code, click on the **Extensions Icon**.
- Search for **Continue** and install it. This is an open-source AI code assistant that works similarly to Copilot.
- After installing, open **Continue** using the extension icon or via the "three dots" menu in VS Code.
- Click on **Configure Continue** to open the JSON configuration file. Replace the default `"llama 3"` model with `"codeQuin"` in the settings, to enable code completion using CodeQuin.

### Step 5: Add Custom Commands

- Add custom commands in the JSON config to provide specific assistance during coding.
  - Example JSON snippet to add a custom command for explaining code step-by-step:
    ```json
    {
      "commands": [
        {
          "command": "step",
          "prompt": "Explain the selected code step by step.",
          "description": "Code explanation"
        }
      ]
    }
    ```
- This custom command allows you to type **"step"** in the Continue chat to get a detailed explanation of highlighted code.

## Usage Examples

### Example 1: JavaScript Date to MySQL Timestamp

- Create a new JavaScript file (`convertToMySQLTimestamp.js`) in VS Code.
- Open the Continue chat window and press `Ctrl + I` (Windows) or `Cmd + I` (Mac) to start generating code.
- Provide the instruction:
  ```
  Write a function that accepts a JavaScript date as a parameter and returns a MySQL timestamp.
  ```
- The generated function might look like this:
  ```javascript
  function convertToMySQLTimestamp(date) {
      return date.toISOString().slice(0, 19).replace('T', ' ');
  }
  ```
- You can highlight the code and ask for improvements (e.g., "Would this be more efficient using `toISOString()`?"). The assistant will provide suggestions accordingly.
- Apply the new version to your current file using the **Apply to Current File** option.

### Example 2: Python REST API Using FastAPI

- Create a new Python file.
- Open the Continue chat and use `Ctrl + I` to request the following:
  ```
  Write a Python REST API using FastAPI and SQLAlchemy.
  ```
- The AI will generate the basic structure for a REST API with **FastAPI** and **SQLAlchemy**. Here’s an example:
  ```python
  from fastapi import FastAPI
  from sqlalchemy import create_engine, Column, Integer, String
  from sqlalchemy.ext.declarative import declarative_base
  from sqlalchemy.orm import sessionmaker

  app = FastAPI()
  DATABASE_URL = "sqlite:///./test.db"
  Base = declarative_base()

  class User(Base):
      __tablename__ = 'users'
      id = Column(Integer, primary_key=True, index=True)
      name = Column(String, index=True)
      age = Column(Integer)

  engine = create_engine(DATABASE_URL)
  SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)

  Base.metadata.create_all(bind=engine)

  @app.get("/users/")
  def read_users():
      session = SessionLocal()
      users = session.query(User).all()
      return users
  ```
- You can review and edit the generated code to suit your needs.

## Summary of Tools and Commands

### Tools Used

- **Ollama**: Manages local AI models.
- **VS Code**: The IDE where you set up the assistant.
- **Continue**: A VS Code extension for interacting with models like **CodeQuin**.

### Commands Recap

- **Verify Installation**: `ollama del`
- **Run Model**: `ollama run codeQuin`
- **Generate Code**: `Ctrl + I` to prompt code generation.
- **Explain Code**: Use custom commands like **"step"** to get explanations.

## Recommendations

- After setup, experiment with different models to determine which one fits your needs.
- Always **review generated code** to ensure it meets your requirements and is free of errors.
- Use these tools to improve productivity, but maintain caution and oversight, especially with complex logic.

## Conclusion

This guide helps you set up a local AI assistant for coding in VS Code using **Ollama**, **Continue**, and **CodeQuin**. The approach offers a **private** and **free** alternative to subscription-based AI assistants like Copilot. It requires a bit of initial setup but can greatly enhance your coding workflow.

Key benefits include keeping your code **local** and **free**, which is crucial for privacy and cost savings. The assistant can assist with everything from code generation to explanations and debugging, making it an effective partner in software development.

[[VSCode]]  [[AI Agents]]  [[Ollama]]