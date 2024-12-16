---
github_link: https://github.com/mshumer/ai-researcher
tags:
- agents
- rag
- python
video-url: https://www.youtube.com/watch?v=AVInhYBUnKs&list=WL&index=16
---

## **Research Agent

The content presented in the video details a step-by-step guide for creating a multi-agent AI research system using OpenAI GPT-based assistants and Autogen for collaboration. Below is a breakdown of the main points, relevant instructions, and potential use cases:

### Overview

The goal is to build a network of AI agents that can autonomously conduct research tasks, quality-assure results, and update an Airtable database. The architecture is scalable, enabling different working groups to be created as needed.

### Key Concepts and Evolution of the AI Researcher System

1. **Initial AI Researcher (May 2023)**: A linear system using large language models (LLMs) to search the web, select relevant links, scrape data, and generate reports based on the research.

    - **Limitation**: Only suitable for simple research; no ability to iteratively refine research based on new information discovered.
2. **Second Version – AI Agents and Task Breakdown**:

    - Introduction of **AI Agents** combining LLMs, memory, and access to tools (e.g., Google Search API).
    - **Goal-Oriented**: Capable of handling ambiguous research goals and autonomously completing tasks by reasoning and using tools.
    - **Improvements**: Enhanced research quality through iterative search and review until adequate information is gathered.
    - **Issues**: Inconsistent quality and limitations in handling constrained tasks (e.g., personal information like phone numbers).
3. **Multi-Agent Systems and Collaboration**:

    - Systems like **MetaGPT** and **ChatDev** introduced frameworks for multiple agents working collaboratively to improve task performance.
    - **Autogen Framework**: A recent tool that allows easier orchestration of complex agent collaborations with various hierarchies and structures.
    - **Cost Reduction**: OpenAI's Assistant API and GPT-4 Turbo have significantly reduced the cost of building and deploying AI agents.
4. **Researcher 3.0 – Structured Multi-Agent System**:

    - **Structure**: Divides roles into **Research Director**, **Research Manager**, and **Research Agent**.
    - **Research Director**: Responsible for extracting tasks from Airtable, breaking down research objectives into smaller subtasks, and delegating work.
    - **Research Manager**: Creates detailed research plans and conducts quality assurance by critiquing and iteratively improving results.
    - **Research Agent**: Executes research tasks, including web searches and scraping, to gather detailed information.

### Fine-Tuning vs. Retrieval Augmented Generation (RAG)

- **Fine-Tuning**: Customizing an AI model to improve its performance on specific tasks (e.g., categorization, email responses).
    - **Challenge**: Requires specialized hardware and large memory.
    - **Gradient AI Platform**: Provides easy fine-tuning of open-source models like **LLaMA 2** with accessible pricing based on token use.
    - **Example Code**: Few lines of code are needed to fine-tune models on Gradient AI, with options to use Node.js, Python, or CLI.
- **Retrieval Augmented Generation (RAG)**: Used to provide up-to-date and accurate information by combining LLMs with a knowledge base.
    - Best suited when providing current, factual data (e.g., stock information).

### Building the System

1. **Tools and Frameworks**:

    - **OpenAI Playground**: Configuring different GPT assistants.
    - **Airtable**: A database to manage the research tasks and results.
    - **Autogen**: Framework for coordinating GPT-based agents.
    - **Browserless.io and SerpAPI**: For web scraping and search capabilities.
2. **Creating Individual GPT Assistants**:

    - **Research Agent**: Implements browsing and scraping, with constraints on iterations and inclusion of research references.
    - **Research Manager**: Responsible for setting research goals and conducting strict quality control.
    - **Research Director**: Interfaces with Airtable to create and update research tasks and delegate responsibilities.
3. **Connecting Agents Using Autogen in Python**:

    - **Setup Configuration**:
        - Store OpenAI and other API keys securely using `.env` files.
    - **Python Code**:
        - Define functions for searching the web, scraping content, summarizing long texts, and interacting with Airtable.
        - Create the agents and set up their roles and capabilities.
        - Use **Autogen** to manage the flow of conversation and task execution between agents.

    Example Code:

    ```python
    `import os from autogen import GPTAssistantAgent, GroupChat  
    # Load environment and config 
    # Define functions for Google search, web scraping, etc.  
    # Create user proxy agent (for user interactions) 
    user_proxy_agent = GPTAssistantAgent(     name="User Proxy",     human_input_mode="always" )  
    # Create research agent 
    researcher_agent = GPTAssistantAgent( name="Researcher", model="gpt-4-
    turbo", assistant_id="YOUR_ASSISTANT_ID" )  
		 # Register functions like Google search,
		  scraping_researcher_agent.register_function(web_scraping) 
		  researcher_agent.register_function(google_search)  
    # Create the research manager and director similarly`
    ```

4. **Running the System**:

    - Use a command like `python app.py` to initiate the AI research team.
    - Monitor conversations and task delegation in the terminal.
5. **Handling Research Tasks**:

    - The system reads records from an Airtable database and assigns research tasks to the appropriate agents.
    - Agents work collaboratively to research, verify information, and update Airtable with accurate results.

### Addressing Issues

- **Memory Management**: Avoiding memory overflow by controlling what information each agent retains.
- **Task Sequencing**: Ensuring that the director assigns tasks one by one to maintain research quality.

### Use Cases

The multi-agent system could be used for:

- **Sales and Venture Capital**: Automated lead qualification and background research.
- **Information Gathering**: Compiling detailed, up-to-date research for various fields.

### Potential for Future Development

- **Customized Memory Structures**: Segmenting memory for different agents to handle specific parts of research without information overload.
- **Scalability**: Creating more agents for other tasks and fine-tuning specific roles as needed.

### Final Note

This approach can become resource-intensive. Monitoring OpenAI usage is essential to control costs.

For further details, examples, and tutorials on building similar systems, consider exploring resources related to OpenAI, Autogen, and tools like Gradient AI for model fine-tuning.

To access the complete code for building a multi-agent research system using GPT-based assistants, you can explore the following GitHub repositories and frameworks:

1. **[MetaGPT](https://github.com/geekan/MetaGPT)**: A multi-agent framework where different roles are assigned to GPTs to collaborate on complex tasks. You can install MetaGPT by running:

 ```bash
    pip install --upgrade metagpt
 ```   
    or clone the repository:
    
```bash
    git clone https://github.com/geekan/MetaGPT && cd MetaGPT && pip install --upgrade -e .
```

    Configuration and usage instructions are detailed in their 
    [documentation(https://docs.deepwisdom.ai/main/en/guide/get_started/configuration.html)​(
    [GitHub](https://github.com/geekan/MetaGPT)).
    
2. **[GPT Researcher](https://github.com/assafelovic/gpt-researcher)**: This agent-based system is designed for online comprehensive research tasks. It utilizes planner and execution agents to gather information from multiple sources and produce detailed reports. Installation involves:

    ```bash
    git clone https://github.com/assafelovic/gpt-researcher.git cd gpt-researcher pip install -r requirements.txt
    ```
    For running the agent, you can use:
    ```bash
    `python -m uvicorn main:app --reload`
    ```
    Visit [the documentation](https://docs.gptr.dev) for full setup instructions, customization options, and examples​([GitHub](https://github.com/assafelovic/gpt-researcher))​ ([GitHub](https://github.com/assafelovic/gpt-researcher/discussions/467)).
    
3. **[AutoGen](https://microsoft.github.io/autogen/)**: A framework developed by Microsoft for building multi-agent AI systems. It provides a high-level abstraction for creating conversational workflows among LLM agents. To get started, you can install AutoGen with:

    ```bash
    `pip install autogen-agentchat~=0.2`
    ```
    You can find additional information about the setup, usage, and examples in the
    [official documentation](https://microsoft.github.io/autogen/)​
    ([GitHub](https://microsoft.github.io/autogen/))​([GitHub](https://github.com/microsoft/autogen)).
    

These resources provide all the necessary code and guidance to build a collaborative AI research system with multiple agents that can work together on complex research tasks autonomously.

[[GPT]]   [[Python]]  [[RAG]]