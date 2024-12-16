---
tags:
  - agents
  - rag
  - python
---

## **Building a Powerful AI Chatbot with Browser Use and Light RAG

### Overview

This video offers a step-by-step guide on building an advanced chatbot using **Light RAG (Retrieval-Augmented Generation)** and a **local large language model (LLM)**, alongside **Browser Use**, an open-source web automation library. This setup creates a versatile AI agent capable of navigating and scraping data from any website and answering questions about the scraped data. The tutorial discusses the weaknesses of traditional RAG systems and how Light RAG addresses these shortcomings with a two-level retrieval system.

### Key Concepts

1. **Light RAG**: Designed to enhance data retrieval by integrating graph structures into text indexing and retrieval, Light RAG uses a **two-level retrieval system**:

    - **Low-Level Search**: Focuses on finding specific entities or relationships.
    - **High-Level Search**: Looks for abstract topics or broader themes.

2. **Browser Use**: An open-source library that allows LLMs to interact with web pages, perform tasks like data scraping, and extract specific information. It can handle multiple tasks, such as:

    - **Detecting Clickable Elements**.
    - **Handling Cookie Prompts** and Popups.
    - **Taking Screenshots** and **Reading Image Content**.
    - **Navigating Across Multiple Tabs**.

### How to Create an AI Agent Using Light RAG and Browser Use

#### Step 1: Set Up the Environment

1. **Install Required Libraries**:

    - Run the command `pip install -r requirements.txt` to install the necessary Python libraries for this project.

2. **Set OpenAI API Key**: The tutorial uses OpenAI’s model, so make sure to **set your OpenAI API key** to enable LLM functionality.

#### Step 2: Import Libraries

- Import the following Python libraries to start:

    ```python
    import browser_use
    import langchain
    import openai
    import light_rag
    ```

#### Step 3: Create the Browser Controller

- The **controller** manages the browser state across multiple agents, allowing them to share browsing sessions:

    ```python
    controller = browser_use.Controller()
    ```

#### Step 4: Initialize Agents

- **Initialize an agent** to find and extract information from Google. Connect it to the **controller** to maintain the browser state:

    ```python
    agent1 = controller.initialize_agent("search_google")
    ```

- **Optional**: Initialize additional agents for multiple tasks:

    ```python
    agent2 = controller.initialize_agent("search_other_site")
    ```

#### Step 5: Define Asynchronous Function for Concurrent Tasks

- Define an asynchronous function to manage multiple tasks simultaneously:

    ```python
    async def run_concurrent_tasks():
        await agent1.run_task()
        await agent2.run_task()
    ```

- Set the **max step limit** for agents:

    ```python
    agent1.set_max_steps(20)
    ```

#### Step 6: Save Extracted Data

- After each step, **save the extracted content** to a file if the task is complete:

    ```python
    if task_completed:
        with open("text.txt", "w") as f:
            f.write(extracted_content)
    ```

#### Step 7: Set Up Working Directory

- Set the **working directory** for Light RAG:

    ```python
    import os
    
    working_dir = "Dickens"
    if not os.path.exists(working_dir):
        os.makedirs(working_dir)
    ```

#### Step 8: Configure Light RAG

- Configure **Light RAG** with appropriate parameters:

    ```python
    light_rag_instance = light_rag.LightRAG(working_dir="Dickens", model="gpt-4.0")
    ```

#### Step 9: Insert and Search Data Using Light RAG

- Insert extracted text into the RAG system:

    ```python
    light_rag_instance.insert("text.txt")
    ```

- Perform different types of searches in Light RAG:
    - **Naive Search**: Direct keyword matching.

        ```python
        light_rag_instance.naive_search("What is supervised fine tuning?")
        ```

    - **Local Search**: Retrieval of direct relationships.

        ```python
        light_rag_instance.local_search("What is supervised fine tuning?")
        ```

    - **Global Search**: Retrieval of both direct and indirect relationships.

        ```python
        light_rag_instance.global_search("What is supervised fine tuning?")
        ```

    - **Hybrid Search**: Combines both local and global relationships.

        ```python
        light_rag_instance.hybrid_search("What is supervised fine tuning?")
        ```

### Key Example

The video demonstrates using Light RAG and Browser Use for real tasks:

1. **Finding the Cheapest Laptop on Amazon**:

    - The agent navigates to **amazon.com** to find laptops meeting specific criteria (e.g., **16GB RAM, GPU RTX 3080 or RTX 4090**).
    - The model self-corrects in case of errors, demonstrating adaptability.

2. **Scraping Google for Supervised Fine-Tuning**:

    - The agent extracts information about **supervised fine-tuning** from Google, using a **vision model** to take screenshots and perform analysis.

### Improvements of Light RAG over Graph RAG

- **Graph RAG** is limited by its higher token usage and multiple API calls.
- **Light RAG** performs retrieval efficiently with:
    - **Dual-Level Retrieval System**: Reducing token usage to under 100.
    - **One API Call** compared to Graph RAG’s multiple calls.
    - **Efficient Handling of Complex Queries**: Light RAG adapts well to dynamic data environments.

### Conclusion

**Light RAG** and **Browser Use** form a powerful combination to create an AI capable of interacting dynamically with the web, providing **contextual, efficient, and accurate responses**. By integrating a **graph-based retrieval system**, Light RAG effectively overcomes the flat data representation and lack of context issues seen in traditional RAG systems. This tutorial showcases an exciting development in the field of AI and web automation, offering users a glimpse into future possibilities for **information search and generation**.

[[RAG]]  [[Python]]