---
tags:
- gpt
---

## **GPT - Researchers

To access the complete code for building a multi-agent research system using GPT-based assistants, you can explore the following GitHub repositories and frameworks:

1. **[MetaGPT](https://github.com/geekan/MetaGPT)**: A multi-agent framework where different roles are assigned to GPTs to collaborate on complex tasks. You can install MetaGPT by running:

```bash
pip install --upgrade metagpt
 ```

    or clone the repository:

```bash
git clone https://github.com/geekan/MetaGPT && cd MetaGPT && pip install --upgrade -e
```  
    Configuration and usage instructions are detailed in their [documentation](https://docs.deepwisdom.ai/main/en/guide/get_started/configuration.html)​([GitHub](https://github.com/geekan/MetaGPT)).
    
2. **[GPT Researcher](https://github.com/assafelovic/gpt-researcher)**: This agent-based system is designed for online comprehensive research tasks. It utilizes planner and execution agents to gather information from multiple sources and produce detailed reports. Installation involves:

    ```bash
    git clone https://github.com/assafelovic/gpt-researcher.git 
    cd gpt-researcher 
    pip install -r requirements.txt
    ```
    For running the agent, you can use:
    ```bash
    python -m uvicorn main:app --reload
   ``` 
3. **[AutoGen](https://microsoft.github.io/autogen/)**: A framework developed by Microsoft for building multi-agent AI systems. It provides a high-level abstraction for creating conversational workflows among LLM agents. To get started, you can install AutoGen with:
    
    bash
    
    Copy code
    ```bash
    pip install autogen-agentchat~=0.2
    ```
    You can find additional information about the setup, usage, and examples in the [official documentation](https://microsoft.github.io/autogen/)​([GitHub](https://microsoft.github.io/autogen/))​([GitHub](https://github.com/microsoft/autogen)).
    

These resources provide all the necessary code and guidance to build a collaborative AI research system with multiple agents that can work together on complex research tasks autonomously.

[[GPT]]  [[Python]] [[AI Agents]]  [[Research Agent]]
