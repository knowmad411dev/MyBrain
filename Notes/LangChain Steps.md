---
Video-URL: https://www.youtube.com/watch?v=8BV9TW490nQ&list=WL&index=3
tags:
- langchain
---

## **LangChain Agents**

### Detailed Summary

In this video, the speaker demonstrates building a LangChain agent using open-source models for language processing and embeddings, specifically the **Mistral (MROL)** model for the language and **Nomic Embed v1.5** for embedding text. The process utilizes various tools to construct an agent, a retrieval model, and a playground for querying text-based documents. Here’s a breakdown of the video:

#### Tools and Frameworks Introduced

1. **LangChain Framework**:

    - A framework for developing applications that leverage language models and embedding models.
    - Offers templates (reference architectures) for building applications, starting with a "retrieval agent template."

2. **Mistral (MROL) Model**:

    - An open-source language model.
    - It can be hosted locally or via the Mistral AI platform. The video uses **Fireworks** as the connector, which includes "Json mode" to enforce structured output.

3. **Nomic Embed v1.5**:

    - A newly released open-source embedding model.
    - Features the ability to set the length and dimensionality of embeddings using a "Mixture of Experts" learning technique.

4. **Chroma DB**:

    - A vector store used to store document embeddings for retrieval.
    - The local persisted version of Chroma is used to store vectors on disk.

5. **LangSmith and LangServe**:

    - **LangSmith**: A debugging and observability tool for LangChain, used to inspect the behavior of agents.
    - **LangServe**: A tool for hosting LangChain templates as REST APIs, allowing easy hosting and testing.

6. **Docusaurus Loader**:

    - A community-contributed document loader for ingesting sections of Docusaurus-generated documentation.

#### Steps to Build the LangChain Agent

1. **Setting Up the LangChain Project**:

    - Navigate to templates.langchain.com and search for the "retrieval agent template."
    - Choose the **Fireworks** version, which uses open-source models. Execute the command:

        ```
        l chain app new
        ```

        - The template generates a `server.py` file with predefined routes.

2. **Modify the Code and Install Dependencies**:

    - Import the default retrieval agent from `langchain.fireworks`.
    - Configure a route to use the retrieval agent (`retrieval agent/fireworks`).
    - Use `Poetry` to manage dependencies:

        ```Python
        poetry install
        poetry run langchain serve
        ```

    - After serving, the playground is accessible at `localhost:8000/retrieval-agent/fireworks/playground`.

3. **Testing the Initial Retrieval Agent**:

    - Query the playground with a question like "What is matka learning?" The system uses an **Archive Retriever** tool, which retrieves academic paper summaries.
    - Use LangSmith to track the agent’s progress and understand which documents are retrieved.

4. **Ingest Custom Documents with Chroma DB**:

    - Create an `ingest.py` script to index specific documentation sections.
    - Import necessary modules:

        ```Python
        from langchain.community.vectorstores import chroma
        from langchain.nomic import nomic_embeddings
        ```

    - Set the **Nomic Embed v1.5** model for embedding:

        ```Python
        embeddings = nomic_embeddings.NomicEmbedTextV1_5()
        ```

    - Configure **Chroma DB** to store vectors:

        ```Python
        vector_store = chroma.Chroma(
            embedding_function=embeddings,
            persist_directory='./chroma_db'
        )
        ```

    - Use the Docusaurus loader to retrieve and index relevant documentation pages:
        - Include dependencies for ingestion:

            ```Python
            poetry add chroma
            poetry run pip install beautifulsoup4 lxml
            ```

        - Filter sitemap URLs to focus on specific sections, e.g., "expression-language."
        - Split long documents into smaller chunks to fit the model's 8,192 token limit:

            ```Python
            from langchain.text_splitter import RecursiveCharacterTextSplitter
            
            text_splitter = RecursiveCharacterTextSplitter(chunk_size=2000, chunk_overlap=100)
            chunk_docs = text_splitter.split_documents(docs)
            ```

    - Add these documents to the vector store:

        ```Python
        vector_store.add_documents(chunk_docs)
        ```

5. **Integrate the Vector Store with the Retrieval Agent**:

    - Modify the retrieval agent in `server.py` to replace the **Archive Retriever** with the **Chroma DB Retriever**.
    - Connect to the persisted Chroma DB:

        ```Python
        retriever = vector_store.as_retriever()
        ```

    - Create a tool for querying the vector store:

        ```Python
        vector_store_tool = Tool(
            name="DocStoreTool",
            func=retriever,
            description="Tool for looking up documentation about the LangChain expression language."
        )
        ```

6. **Test the Updated Retrieval Agent**:

    - Use the playground to ask questions about the indexed documentation.
    - For example, ask, "What is a runnable pass-through?" The agent retrieves the appropriate documentation section and provides an answer.
    - You can track the calls and see the retrieved documents in LangSmith.

#### Lessons Learned and Future Improvements

- **Document Cleaning and Relevance**: The results highlight the importance of carefully choosing which documents to index and ensuring they are well-prepared for effective retrieval.
- **Prompt Engineering**: Fine-tuning prompts for specific queries can enhance the relevance and accuracy of retrieved information.
- **Optional Improvements**: Clean up documents by filtering irrelevant content like sidebars or navigation menus before ingestion.

#### Conclusion

- The video demonstrates how to set up a LangChain agent that uses open-source models for language and embeddings.
- A combination of tools, including Chroma DB, LangSmith, and LangServe, is used to build and test the retrieval agent.
- Additional enhancements like prompt engineering and document filtering are mentioned for future work to improve accuracy and relevance.

[[LangChain]] | [[AI Agents]] | [[Python]] | [[LLM]] | [[LLM Frameworks]]