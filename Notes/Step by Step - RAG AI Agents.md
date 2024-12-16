---
tags:
- rag
- agents
video-url: https://www.youtube.com/watch?v=wEXrbtqNIqI&list=WL&index=4
---

## **Step by Step - RAG AI Agents

**Overview:**

The video is about building a more production-ready RAG (Retrieval-Augmented Generation) AI agent system. It involves using PostgreSQL and Supabase for data management and retrieval. The presenter goes through the steps for creating the RAG system, focusing on how to use Supabase, Google Drive triggers, PostgreSQL, and vector databases to create a flexible and reliable knowledge management setup. This new approach is compared against other RAG builds that use tools like Pinecone, to explain the advantages of PostgreSQL and Supabase for improved data safety and scalability.

**Key Concepts:**

1. **Retrieval-Augmented Generation (RAG):** RAG combines retrieval and generation to enhance the response capability of an AI agent. The system retrieves relevant information from a database or knowledge base and then generates an appropriate response.
2. **Components:**
   - **Supabase:** A backend platform with built-in relational databases, used here for vector storage and to store chat histories.
   - **PostgreSQL:** Used to handle chat memory, offering data safety, persistence, and the ability to scale for larger data sets.
   - **Vector Database:** Stores documents in a format that makes it easy to search for semantically similar information.

**System Breakdown: RAG AI Agent Overview**

- The system starts with a question from the user. The AI agent needs to retrieve relevant information before generating a response. The retrieval component ensures that the AI has the proper context, while the generative component provides a coherent and useful answer to the user's question.
- **Old vs. New Setup**: The previous build used window buffer memory and Pinecone, but the current setup uses PostgreSQL for memory and Supabase for storage. The key improvement is around data safety, persistence, and better scaling.
- **Use Case**: The RAG system is used to interact with uploaded documents and respond to questions based on their content. For the demo, a sample project called "Project Mountain" was used to illustrate the workflow of asking the AI about the project's action items and involved parties.

**Steps to Build the RAG System:**

1. **Setting Up Supabase:**
   - Create a Supabase account and set up a new project.
   - You need to provide a project name and create a secure password, which will be used later for various configurations.
   - Once the project is set up, navigate to **Project Settings > Database** to obtain information like the host, port, user, and password needed to connect PostgreSQL to your system.

2. **Connecting Supabase to the AI Agent**
   - The AI agent needs a system prompt to guide it on how to use the vector database to retrieve information.
   - Set up OpenAI's language model (in this case, GPT-4 Mini) to handle responses based on the vector data stored in Supabase.
   - Use **PostgreSQL** as the memory system. You need to configure a PostgreSQL connection with credentials obtained from Supabase.

3. **PostgreSQL vs. Window Buffer Memory:**
   - **PostgreSQL Advantages**:
     - **Data Safety and Persistence**: Even if the system restarts, the memory remains intact, which is not the case with window buffer memory.
     - **Scalable for Big Data**: PostgreSQL can handle larger datasets and perform efficient searches using indexing.
   - **Window Buffer Memory**: Although simpler and easier to set up, it's not ideal for long-term use due to its temporary nature.

4. **Supabase vs. Pinecone:**
   - **Supabase**: Best suited for small to medium-scale projects due to its combination of relational and vector storage capabilities.
   - **Pinecone**: More suitable for large-scale projects with billions of vectors due to its managed vector database and scalability.
   - **Hosting**: Supabase offers both managed and self-hosted options, whereas Pinecone is available only as a SaaS platform.

5. **Configuring the Workflow: Retrieving and Updating Data**
   - **Adding Documents to Vector Store**:
     - Use Supabase's SQL editor to set up tables for storing documents and chat history.
     - The presenter shows how to add a document to the vector store by configuring an embedding using **text-embedding-ada-003**.
   - **Memory and Chat History**: Each interaction is stored in Supabase to provide a consistent context for ongoing chats.

6. **Automating File Management using Google Drive**
   - **Google Drive Triggers**: The workflow begins by adding a **Google Drive trigger** that monitors for any new or updated files in a specific folder. This automates the ingestion of new project documents into the RAG system.
   - **Workflow for New Files**:
     - When a new file is added, it triggers a sequence of actions:
       1. The file ID is fetched.
       2. The file is downloaded and converted to text.
       3. The extracted content is then added to the vector store in Supabase.
   - **Handling Updates**: A similar workflow is created for when files are updated. The old version is deleted from Supabase, and the new one is added to keep the information up-to-date.

7. **Practical Demonstration of RAG Agent**
   - The presenter tested the setup by asking questions about "Project Mountain." Initially, the system could not return any information until the document was added to the vector store.
   - After uploading "Project Mountain," the AI was able to respond accurately to queries about action items, involved parties, and budget.

8. **Setting Up the Agent in Supabase**
   - The system prompt is configured to inform the agent that it should retrieve information from the vector database.
   - In the setup, **embedding-ada-003** is used as the default embedding model, which allows the system to convert text into vector representations that can be searched and compared.

9. **Testing and Demonstrating the System**
   - The presenter demonstrated the process of adding a new document ("Project Snow") and tested if the system could correctly recognize the information.
   - After making changes to the document (e.g., updating the budget), the changes were correctly reflected in the RAG agent's responses, demonstrating the success of the update workflow.

**Tips and Tricks Shared in the Video:**

- **Automating Data Updates**: Use a combination of Google Drive triggers and Supabase workflows to automate updates whenever a new file is added or an old file is changed.
- **Embedding Options**: You can use **text-embedding-ada-003** to add documents to the vector store efficiently. It helps ensure the embedding aligns well with the type of queries being made.
- **Keeping Memory Accurate**: Whenever a file is updated, the old version is deleted, and the new one is added to keep the stored data current. This helps in maintaining trust in the system's responses.

**Final Recommendations:**

- **Supabase for Medium-Scale Use**: The presenter recommended Supabase for smaller to medium-scale projects due to its flexibility, while Pinecone might be better suited for larger projects that require more extensive vector storage.
- **Hands-On Learning**: The presenter mentioned their community where they provide downloadable workflows and paid hands-on sessions for those looking to implement these kinds of systems in their businesses or learn more deeply.
- **Further Automations**: Suggested adding additional Google Drive triggers for file deletions to maintain vector store cleanliness, ensuring only up-to-date information is accessible.

**Conclusion:**

The video offers a comprehensive guide to building a RAG AI agent using PostgreSQL and Supabase, with additional tools like Google Drive for automation. The solution aims for greater scalability, persistence, and data safety compared to simpler window buffer memory approaches, and uses modern backend tools to enhance both usability and automation in AI-assisted workflows. The walkthrough includes practical examples, detailed explanations of configurations, and real-time demonstrations to illustrate the functionality of the setup.

[[RAG]]