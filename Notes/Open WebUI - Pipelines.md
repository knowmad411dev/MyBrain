---
github_link: https://github.com/casedone
tags:
- python
- ollama
- automation
video-url: https://www.youtube.com/watch?v=uTDeuxyN-RM&list=WL&index=2
---

## **Open WebUI - Pipelines

### Overview of Open Web UI Pipelines and How-To Instructions

This document summarizes the key points from a video explaining the usage of pipelines in Open Web UI, including code examples, instructions, and use cases.

---

### **Introduction to Open Web UI Pipelines**

Pipelines in Open Web UI are described as a robust framework for customizing workflows, integrating external systems, and enabling advanced functionalities. Key features include:

- **Customization**: Allows implementation of custom Python code.
- **Integration**: Supports external models, databases, and APIs (e.g., Google, non-OpenAI providers).
- **Modularity**: Structures workflows into logical components like Inlet, Outlet, and Pipe.

---

### **Setup Instructions**

1. **Clone the Repository**:
   - Visit the GitHub repository for Open Web UI pipelines.
   - Clone the repository to your local machine.

   ```bash
   git clone https://github.com/openwebui/pipelines.git
   cd pipelines
   ```

2. **Directory Structure**:
   - **Examples**: Contains sample pipelines and filters.
   - **Scaffold**: For managing multiple pipelines together.
   - **Pipelines Folder**: Add custom pipelines here.

3. **Local Development**:
   - Develop pipelines in Python using the provided structure.
   - Drop your custom Python files into the `pipelines` folder for execution.

4. **Running the Pipeline Server**:
   - Start the pipeline server to make your custom pipelines available in Open Web UI.

   ```bash
   python -m openwebui.pipeline_server
   ```

5. **Using Docker**:
   - If using Docker, upload new pipeline files manually via the admin page.
   - This can be tedious; cloning the repo locally is recommended for efficiency.

---

### **Pipeline Structure**

A pipeline consists of the following components:

- **Class Definition**: Define a class for your pipeline.
- **Initialization (`__init__`)**:
  - Name your pipeline.
  - Initialize `valves` and other parameters.
- **Optional Functions**:
  - `on_startup`, `on_shutdown`, and `on_valve_update` for custom initialization and cleanup.
- **Main Functionality (`pipe`)**:
  - Core logic is implemented here.
- **Filters (Inlet & Outlet)**:
  - Optional; used for preprocessing and postprocessing messages.

#### Example Template:

```python
class CustomPipeline:
    def __init__(self):
        self.name = "example_pipeline"
        self.valve = None  # Initialize valves if needed

    def on_startup(self):
        pass

    def on_shutdown(self):
        pass

    def pipe(self, user_message):
        # Core logic here
        return f"Processed: {user_message}"
```

---

### **Examples**

#### **1. Translation Pipeline**

Translates a user message from a source language to English and back to the target language.

```python
class TranslationPipeline:
    def __init__(self):
        self.name = "llm_translate"

    def pipe(self, user_message):
        # Mock translation logic
        source_language = "auto-detect"
        target_language = "English"
        translated_message = self.translate(user_message, source_language, target_language)
        return translated_message

    def translate(self, message, source, target):
        # Replace with actual translation logic
        return f"Translated [{source} -> {target}]: {message}"
```

---

#### **2. Prefixer Pipeline**

Adds a prefix to user messages.

```python
class PrefixerPipeline:
    def __init__(self):
        self.name = "prefixer"

    def pipe(self, user_message):
        prefix = "CustomPrefix: "
        return prefix + user_message
```

---

#### **3. Basic Data Retrieval Pipeline**

Retrieves descriptions for predefined data keys (e.g., coffee types).

```python
class BasicRetrievalPipeline:
    def __init__(self):
        self.name = "basic_retrieval"

    def create_data_dict(self):
        return {
            "gisha": "Gisha coffee is rich and smooth.",
            "blue_mountain": "Blue Mountain coffee is a premium choice."
        }

    def pipe(self, user_message):
        data_dict = self.create_data_dict()
        if user_message.lower() in data_dict:
            return data_dict[user_message.lower()]
        return "Cannot find product in database."
```

---

### **Integration with Open Web UI**

1. **Add Pipeline to Admin**:
   - Navigate to the admin page of Open Web UI.
   - Upload your Python file to register the pipeline.

2. **Select Pipeline in Chat**:
   - Choose your pipeline from the dropdown menu in the model selection.

3. **Test Your Pipeline**:
   - Input test messages to verify functionality.

---

### **Advanced Features**

1. **Complex Logic in Pipes**:
   - Integrate external databases (e.g., SQL, vector embeddings).
   - Chain multiple models or APIs within the `pipe` function.

2. **Multi-Agent Systems**:
   - Incorporate additional agents (e.g., LLMs, retrieval systems) for advanced processing.

3. **Non-OpenAI Integration**:
   - Examples for integrating models like Gemini or Anthropic are available in the examples folder.

---

### **Tips for Efficient Development**

- **Avoid Docker Complexity**:
  - Use local development for rapid iteration.
- **Focus on `pipe` Logic**:
  - Start simple; gradually add complexity.
- **Use Examples**:
  - Study the example pipelines in the repository for inspiration.

---

### **Conclusion**

Pipelines in Open Web UI offer a powerful framework for building custom workflows. By leveraging its modular design and integration capabilities, developers can create everything from simple transformations to advanced multi-agent systems. The provided examples serve as a starting point for your exploration.

[[Ollama]]  [[Open Web UI]]  [[Workflow]]