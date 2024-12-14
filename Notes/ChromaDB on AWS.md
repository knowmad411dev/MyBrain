---
Video-URL: https://www.youtube.com/watch?v=F6yXY0F8lig&list=WL&index=6
tags:
- chromadb
- database
---

# How to Deploy ChromaDB as a Server Instance on AWS EC2 Using Docker

ChromaDB is a vector database that allows for efficient storage and retrieval of embeddings, making it ideal for applications involving natural language processing and similarity search. While you can use ChromaDB as a local library, deploying it as a server instance provides the flexibility to access it from anywhere, including from Google Colab notebooks or multiple client applications.

In this guide, we'll walk through the steps to deploy [[ChromaDB]] on an [[AWS EC2]] instance using [[Docker]]. We'll cover how to set up the EC2 instance, install Docker, run the ChromaDB Docker image, and connect to the ChromaDB server from a client.

---

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Step 1: Launch an AWS EC2 Instance](#step-1-launch-an-aws-ec2-instance)
3. [Step 2: Connect to Your EC2 Instance](#step-2-connect-to-your-ec2-instance)
4. [Step 3: Install Docker on the EC2 Instance](#step-3-install-docker-on-the-ec2-instance)
5. [Step 4: Pull and Run the ChromaDB Docker Image](#step-4-pull-and-run-the-chromadb-docker-image)
6. [Step 5: Configure AWS Security Group to Allow Port 8000](#step-5-configure-aws-security-group-to-allow-port-8000)
7. [Step 6: Verify ChromaDB Server is Running](#step-6-verify-chromadb-server-is-running)
8. [Step 7: Connect to ChromaDB Server from a Client](#step-7-connect-to-chromadb-server-from-a-client)
9. [Step 8: Use Custom Embeddings (Optional)](#step-8-use-custom-embeddings-optional)
10. [Step 9: Run Docker Container in Detached Mode](#step-9-run-docker-container-in-detached-mode)
11. [Step 10: Troubleshooting Common Issues](#step-10-troubleshooting-common-issues)
12. [Conclusion](#conclusion)
13. [Useful Links](#useful-links)

---

## Prerequisites

- **AWS Account**: Access to AWS with permissions to create EC2 instances.
- **Basic Knowledge**: Familiarity with AWS EC2, Docker, and Python.
- **SSH Client**: To connect to the EC2 instance (e.g., Terminal, PuTTY).
- **Key Pair File**: `.pem` file for SSH access to the EC2 instance.

---

## Step 1: Launch an AWS EC2 Instance

1. **Navigate to EC2 Service**:

    - Log in to your AWS Management Console.
    - Search for **EC2** and open the EC2 Dashboard.
2. **Launch Instance**:

    - Click on **"Launch Instance"**.
3. **Configure Instance Details**:

    - **Name**: Set a recognizable name (e.g., `chroma-db`).
    - **AMI**: Choose **Ubuntu Server 20.04 LTS (HVM), SSD Volume Type**.
    - **Instance Type**: Select an instance with at least **2 GB RAM** (e.g., `t3.small` or `t2.medium`).
    - **Key Pair**: Create a new key pair or use an existing one.
        - If creating a new key pair:
            - Click **"Create new key pair"**.
            - Enter a name (e.g., `chroma-db-key`).
            - **Key pair type**: `RSA`.
            - **Private key file format**: `PEM`.
            - Click **"Create key pair"** and save the `.pem` file securely.
    - **Network Settings**:
        - By default, SSH (port 22) is allowed. We'll add port 8000 later.
    - **Configure Storage**:
        - Adjust the storage size if needed (e.g., increase to **16 GB**).
    - **Advanced Details**:
        - Leave as default unless you have specific requirements.
4. **Launch Instance**:

    - Review your settings.
    - Click **"Launch Instance"**.
    - Wait for the instance to be in the **"Running"** state.

---

## Step 2: Connect to Your EC2 Instance

1. **Locate Public IP**:

    - In the EC2 Dashboard, click on **"Instances"**.
    - Select your instance.
    - Note the **Public IPv4 address** (e.g., `3.123.456.789`).
2. **Set Permissions on Key Pair File** (if on Unix/MacOS):

    - Open a terminal where your `.pem` file is located.
    - Run:

```bash
        chmod 400 chroma-db-key.pem
      ```
 
3. **Connect via SSH**:
    
    - Run:
        
```bash
        ssh -i /path/to/chroma-db-key.pem ubuntu@<your_ec2_public_ip>
     ```
  
        Replace `/path/to/chroma-db-key.pem` with the path to your key file and `<your_ec2_public_ip>` with the actual IP.
        
    - Example:
        
        
```bash
        ssh -i ~/Downloads/chroma-db-key.pem ubuntu@3.123.456.789
      ```
 
    - If prompted, type **"yes"** to continue connecting.
        

---

## Step 3: Install Docker on the EC2 Instance

1. **Update Package Lists**:
    

```bash
    sudo apt update
 ```

2. **Install Prerequisite Packages**:

```bash
    sudo apt install apt-transport-https ca-certificates curl software-properties-common
  ```

3. **Add Docker’s GPG Key**:

```bash
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
 ```

4. **Add Docker Repository**:

```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
 ```

5. **Update Package Lists Again**:

```bash
    sudo apt update
  ```

6. **Install Docker CE (Community Edition)**:

```bash
    sudo apt install docker-ce
 ```

7. **Verify Docker Installation**:

```bash
    docker --version
 ```

    - Expected output: `Docker version XX.XX.X, build XXXXXXX`

---

## Step 4: Pull and Run the ChromaDB Docker Image

1. **Pull ChromaDB Docker Image**:

```bash
    sudo docker pull chromadb/chromadb:latest
   ```

2. **Run the Docker Container**:

```bash
    sudo docker run -d -p 8000:8000 chromadb/chromadb:latest
 ```

    - `-d`: Runs the container in detached mode.
    - `-p 8000:8000`: Maps port 8000 of the host to port 8000 of the container.
3. **Verify the Container is Running**:

```bash
    sudo docker ps
 ```

    - You should see a container running with the `chromadb/chromadb` image.

---

## Step 5: Configure AWS Security Group to Allow Port 8000

1. **Navigate to Security Groups**:

    - In the EC2 Dashboard, select your instance.
    - Click on the **"Security"** tab.
    - Click on the associated **Security Group ID**.
2. **Edit Inbound Rules**:

    - Click **"Edit inbound rules"**.
3. **Add a New Rule**:

    - **Type**: Custom TCP
    - **Protocol**: TCP
    - **Port Range**: `8000`
    - **Source**: `0.0.0.0/0` (Anywhere) or restrict to your IP for better security.
    - **Description**: `Allow ChromaDB access`
4. **Save Rules**:

    - Click **"Save rules"**.

---

## Step 6: Verify ChromaDB Server is Running

1. **Access ChromaDB API Docs**:

    - Open a web browser.
    - Navigate to:

```arduino
        http://<your_ec2_public_ip>:8000/docs
   ```   

        Replace `<your_ec2_public_ip>` with your instance's public IP.
1. **Check API Documentation**:

    - You should see the ChromaDB API documentation powered by **FastAPI**.
    - If you see the documentation, the server is running correctly.

---

## Step 7: Connect to ChromaDB Server from a Client

We'll demonstrate how to connect to the ChromaDB server from a Google Colab notebook.

1. **Open Google Colab**:

    - Go to Google Colab and open a new notebook.
2. **Install ChromaDB Client**:

```bash
    !pip install chromadb
```

3. **Import ChromaDB and Connect to Server**:

```python
    import chromadb  
    client = chromadb.HttpClient(host="<your_ec2_public_ip>", port=8000)
```

4. **Create a Collection**:

```python

    collection = client.create_collection(name="test_collection")
  ```  
5. **Add Documents to the Collection**:

```python
collection.add(documents=["This is a document about cats.", "This is a document about cars."],     
	metadatas=[{"category": "animal"}, {"category": "vehicle"}],     ids=["doc1", "doc2"] )
 ```   
6. **Query the Collection**:

```python
results = collection.query(query_texts=["Tell me about dogs"], n_results=1 )  print(results)
 ```   
    - Expected output:
        
```lua 
{'ids': [['doc1']], 'distances': [[...]], 'documents': [['This is a document about cats.']], 'metadatas': [[{'category': 'animal'}]]}
 ```       
    - The document about cats is returned because it's semantically similar to dogs.
        

---

## Step 8: Use Custom Embeddings (Optional)

By default, ChromaDB uses a built-in embedding model. If you wish to use a custom embedding model (e.g., OpenAI's embeddings or Sentence Transformers), you can specify it when creating the client or collection.

**Example with Custom Embedding Function**:

```python
from chromadb.utils import embedding_functions  
# Use OpenAI embedding function 
openai_ef = embedding_functions.OpenAIEmbeddingFunction(     api_key="your_openai_api_key", model_name="text-embedding-ada-002" )  
client = chromadb.HttpClient( host="<your_ec2_public_ip>", port=8000,     embedding_function=openai_ef )  collection = client.create_collection(name="test_collection")
```

**Note**: Replace `"your_openai_api_key"` with your actual OpenAI API key.

---

## Step 9: Run Docker Container in Detached Mode

Running the Docker container in detached mode allows you to continue using the terminal after starting the container.

1. **Stop Existing Container** (if running without `-d`):

```bash
    sudo docker ps
  ```

    - Note the `CONTAINER ID` of the ChromaDB container.
    
```bash
    sudo docker stop <container_id>
 ```

2. **Run Container in Detached Mode**:

```bash
    sudo docker run -d -p 8000:8000 chromadb/chromadb:latest
 ```

3. **Verify Container is Running**:

```bash
    sudo docker ps
 ```

    - The container should be listed and running.

---

## Step 10: Troubleshooting Common Issues

- **Permission Denied Errors**:
    - If you encounter permission errors when running Docker commands, prefix commands with `sudo`.
- **Port Already in Use**:
    - If you receive an error that port 8000 is already in use:
        - Check running processes:

```bash
            sudo lsof -i :8000
 ```

        - Kill the process using the port:
            
```bash
            sudo kill <pid>
  ```

- **Connection Timeouts**:
    - Ensure the security group allows inbound traffic on port 8000.
    - Verify the ChromaDB server is running.
- **SSH Permission Issues**:
    - If SSH complains about permissions on your `.pem` file, adjust the permissions:

```bash
        chmod 400 /path/to/chroma-db-key.pem
 ```

---

## Conclusion

By following this guide, you've successfully deployed ChromaDB as a server instance on an AWS EC2 instance using Docker. This setup allows you to access ChromaDB from anywhere, enabling seamless integration with various applications and clients. You can now store, manage, and query your vector data efficiently and scale your applications accordingly.

---

## Useful Links

- **ChromaDB GitHub Repository**: [https://github.com/chroma-core/chroma](https://github.com/chroma-core/chroma)
- **ChromaDB Documentation**: https://docs.trychroma.com/
- **Docker Installation Guide for Ubuntu**: https://docs.docker.com/engine/install/ubuntu/
- **AWS EC2 Documentation**: [https://docs.aws.amazon.com/ec2/index.html](https://docs.aws.amazon.com/ec2/index.html)
- **Beginner Tutorial on ChromaDB**:
    - _Note_: In the original video, the speaker refers to a previous tutorial. You can find tutorials on ChromaDB usage in their documentation or community resources.

 [[Linux]]  [[ChromaDB Vector Database]]  [[Python]]