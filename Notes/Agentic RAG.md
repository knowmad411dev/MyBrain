---
tags:
- rag
- agents
video-url: https://www.youtube.com/watch?v=kkF9gsBF7gg&list=WL&index=2
---

## **Agentic [[RAG]]

### Detailed Overview: Implementing Agentic RAG with Fi Data

This detailed overview provides a comprehensive look at agentic RAG (Retrieval-Augmented Generation), focusing on the future of AI knowledge systems and how they surpass traditional RAG systems in both capabilities and efficiency. The goal is to help you understand agentic RAG, why it matters, and how to implement it using Fi Data. Below, you'll find a breakdown of both the theory and the practical steps needed to build an agentic RAG, complete with code examples.

#### **What is Agentic RAG?**

Agentic RAG is a more advanced version of the traditional Retrieval-Augmented Generation (RAG) system. It moves beyond simply querying a knowledge base by introducing autonomous, adaptive capabilities for knowledge retrieval. Unlike traditional RAG systems that struggle with complex, multi-faceted queries, agentic RAG introduces autonomous knowledge navigation, multisource intelligence, and self-improving retrieval, making it far more effective at tackling challenging questions.

**Key Differences:**
- **Traditional RAG**: Limited to single-source retrieval, static query processing, and lacks a validation layer. It performs indexing and querying to retrieve chunks of relevant information, then passes this data to a large language model ([[LLM]]).
- **Agentic RAG**: Adds intelligent agents that manage query decomposition, relevance checking, hallucination control, and retrieval tools access. It can break down complex queries into simpler components for precise results, ultimately improving accuracy.

#### **Implementing Agentic RAG Step-by-Step**

##### **Step 1: Setting up the Environment**

1. **Install Fi Data and Related Packages**: To begin, open your terminal and execute the following command:
    ```bash
    pip install fi_data
    ```
2. **Export [[OpenAI]] API Key**: Since we're using GPT-4, we need to authenticate with OpenAI.
    ```bash
    export OPENAI_API_KEY='your_openai_api_key_here'
    ```

    Visit [platform.openai.com](https://platform.openai.com) to generate your API key.

3. **Install PostgreSQL Using Docker**: We need PostgreSQL for chat history storage.
    - **Install Docker**: Download and install Docker based on your operating system from [Docker's website](https://www.docker.com).
    - **Run PostgreSQL Container**: Run the following command to create a PostgreSQL database with vector capabilities.
      ```bash
      docker run -d --name pg-vector -e POSTGRES_PASSWORD=mysecretpassword -p 5432:5432 ankane/pgvector
      ```
    - **Check Status**: Verify PostgreSQL is running by typing:
      ```bash
      docker ps
      ```

##### **Step 2: Creating a Traditional RAG System**

1. **Create Python File**: Start by creating a [[Python]] script called `app.py`.
    ```bash
    touch app.py
    ```
2. **Import Necessary Libraries**:
    ```python
    from fi_data.agent import Agent
    from fi_data.openai_chat import OpenAIChat
    from fi_data.openai_embed import PDFKnowledgeBase
    from fi_data.pg_agent_storage import PGVector
    from fi_data.playground import Playground
    ```
3. **Connect to PostgreSQL Database**:
    ```python
    connection_string = "postgresql://localhost:5432/ai_database"
    pg_storage = PGVector(connection_string)
    ```
4. **Set Up Knowledge Base**:
    - Index data from a PDF to populate the vector database.
    ```python
    knowledge_base = PDFKnowledgeBase.load("my_data.pdf", storage=pg_storage, search_type="hybrid")
    ```
5. **Define and Use the Agent**:
    - Create a traditional RAG agent.
    ```python
    agent = Agent(knowledge_base=knowledge_base, search_knowledge=False)
    response = agent.ask("How do I make chicken and galangal in coconut milk soup?")
    print(response)
    ```
6. **Execute the Python Script**:
    ```bash
    python app.py
    ```
    - The system will index the data and answer a simple question, showing the typical RAG behavior.

##### **Step 3: Implementing Agentic RAG**

1. **Introduce Query Decomposition**:
    - Modify the agent to add autonomous features for complex queries by enabling `search_knowledge`.
    ```python
    agent = Agent(knowledge_base=knowledge_base, search_knowledge=True)
    complex_query = "I want to make a three-course meal with soup, Thai curry, and dessert. Can you recommend recipes?"
    response = agent.ask(complex_query)
    print(response)
    ```
    - **Query Decomposition**: The agent will automatically break down the query into smaller parts (e.g., soup recipes, curry recipes, dessert recipes) and search accordingly.

##### **Step 4: Creating a User Interface**

1. **Set Up Playground**:
    - Initiate the UI component with `Playground` for better interaction.
    ```python
    app = Playground(agent=agent, read_chat_history=True)

    if __name__ == "__main__":
        knowledge_base.load()
        app.run()
    ```
2. **Run and Access UI**:
    ```bash
    python app.py
    ```
    - You will receive a URL to access a UI for interacting with the agent.

#### **Benefits and Drawbacks of Agentic RAG**

**Benefits**:
- **Accuracy**: More accurate responses due to query decomposition and validation.
- **Autonomy**: Performs tasks automatically without the need for user prompts.
- **Human Collaboration**: Improves interaction quality through context maintenance.
- **Improved Information Quality**: Access to multiple data sources for richer responses.

**Drawbacks**:
- **Latency**: Increased processing time due to query decomposition.
- **System Complexity**: Adds complexity to the overall architecture.
- **Resource Intensive**: Requires powerful hardware and appropriate LLM configuration to avoid hallucinations and ensure reliability.

#### **Conclusion**

With Agentic RAG, AI knowledge systems are evolving from simple information retrieval to intelligent, autonomous assistants capable of handling complex questions effectively. While the increased system complexity and resource requirements are challenges, the significant improvements in accuracy, autonomy, and human collaboration make agentic RAG a valuable tool for the future of AI.

Stay tuned for more tutorials, and check out additional content for implementing more complex AI agents using Fi Data!

[[RAG]]  [[AI Agents]]  [[Python]] 