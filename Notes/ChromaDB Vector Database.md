---
Video-URL: https://www.youtube.com/watch?v=61kaK-e3Owc&list=WL&index=3
tags:
- chromadb
- database
---

# How to Run ChromaDB Vector Database

## Summary

In this video, Timothy Kbat, founder of MLEx Labs, provides an updated tutorial on setting up and using [[ChromaDB]], a vector database for handling embeddings and retrieval, as of its latest release (v0.4.18 on November 21st, 2023). He covers the installation using Docker, data persistence between container updates, and setting up authentication for securing API access.

## Key Steps Covered

### 1. [[ChromaDB]] Installation via [[Docker]]

- **Requirement**: Ensure Docker is installed and running.
- **Pull the latest ChromaDB image** from Docker Hub using the terminal command:

    ```bash
    docker pull chromadb/chroma
    ```

- **Run the ChromaDB container** on a local machine:

    ```bash
    docker run -p 8000:8000 chromadb/chroma
    ```

    This runs a container exposing port 8000, which is ChromaDB's default port for API access.

### 2. Confirming the Running ChromaDB Instance

- After starting the container, visit `http://localhost:8000/api/v1/` in the browser to verify that ChromaDB is running. A response with `"nan"` in the heartbeat means it’s running correctly.

### 3. Persisting Data Across Docker Container Updates

- Running ChromaDB directly via the above method saves data inside the container, which is lost upon container deletion or version update.
- To **persist data** and maintain it across different container versions, create a volume on your host machine:

    ```bash
    mkdir ~/chroma_data
    cd ~/chroma_data
    ```

- **Mount the host directory** to the container’s internal data directory:

    ```bash
    docker run -p 8000:8000 -v ~/chroma_data:/chroma/chroma chromadb/chroma
    ```

    This method mounts `~/chroma_data` on your host machine to `/chroma/chroma` inside the container. As a result, the data is saved to the host machine, and new containers using this volume will have access to the existing data.

### 4. Testing Data Persistence

- After creating and uploading embeddings (e.g., using a tool like AnythingLLM to upload PDFs or documents to ChromaDB), you can **stop and delete the container**:

    ```bash
    docker stop <container_id>
    docker rm <container_id>
    ```

- **Start a new container** with the same volume mounted:

    ```bash
    docker run -p 8000:8000 -v ~/chroma_data:/chroma/chroma chromadb/chroma
    ```

- Visit the API endpoint again to see that your collections and embeddings persist.

### 5. Setting Up Authentication

- ChromaDB now supports built-in authentication, providing an extra layer of security for API access.
- To **enable an API key-based token system**, set the environment variables when starting the Docker container:

    ```bash
    docker run -p 8000:8000 -v ~/chroma_data:/chroma/chroma \
      -e CHROMA_SERVER_AUTH_PROVIDER=chromadb.auth.token \
      -e CHROMA_SERVER_AUTH_CREDENTIALS=<token> \
      chromadb/chroma
    ```

    Replace `<token>` with your desired API key.

- With this setup, you need to include the `X-Chroma-Token: <token>` header in your API requests.

### 6. Testing Authentication

- To verify, use a tool like Postman to send a GET request to the ChromaDB endpoint `http://localhost:8000/api/v1/collections`. Without the correct token in the header, you'll receive a 401 Unauthorized error.
- Adding the correct token header allows you to access your collections:

    ```bash
    X-Chroma-Token: <token>
    ```

### 7. Updating Tokens and Rebooting Containers

- If the token or environment variables need to be updated, delete the running container and restart it with the updated variables.
- Data stored in the mounted volume persists, so only the token changes, ensuring secure access.

### 8. Deploying to Cloud Services

- The video concludes with a teaser for deploying ChromaDB on cloud platforms like AWS or Render, promising future tutorials to cover the deployment process and securing access in a similar way as the local setup.

## Resources

- **ChromaDB GitHub**: [GitHub Repository](https://github.com/chromadb/chroma)
- **ChromaDB Documentation**: Chroma Docs
- **Docker Hub Image**: Docker Hub - ChromaDB
- **AnythingLLM**: A tool that integrates with ChromaDB for embedding document data (likely available via GitHub or its official site).

## How-To Instructions

### 1. Install Docker

- Download and install Docker from Docker’s official site.

### 2. Pull and Run ChromaDB

- Open terminal and run:

    ```bash
    docker pull chromadb/chroma
    docker run -p 8000:8000 chromadb/chroma
    ```

### 3. Persist Data

- Create a directory for ChromaDB data:

    ```bash
    mkdir ~/chroma_data
    ```

- Run ChromaDB with the volume mount:

    ```bash
    docker run -p 8000:8000 -v ~/chroma_data:/chroma/chroma chromadb/chroma
    ```

### 4. Set Authentication (Optional)

- Run ChromaDB with authentication enabled:

    ```bash
    docker run -p 8000:8000 -v ~/chroma_data:/chroma/chroma \
      -e CHROMA_SERVER_AUTH_PROVIDER=chromadb.auth.token \
      -e CHROMA_SERVER_AUTH_CREDENTIALS=<token> \
      chromadb/chroma
    ```

    Replace `<token>` with your secure API key.

---

This guide offers a detailed walkthrough for setting up ChromaDB locally with Docker, ensuring data persistence, and adding secure API key access, with promises of future content for cloud deployment.

[[Vector Databases]]  [[ChromaDB on AWS]]
