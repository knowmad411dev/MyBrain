---
tags:
- cloud
video-url: https://www.youtube.com/watch?v=259KgP3GbdE&list=WL&index=15
---

## **Cloud-Deployed AI App**

### **Deploying AI Applications to the [[Cloud]]: A Comprehensive Guide**

In this detailed tutorial, the presenter walks through deploying AI applications to the cloud using **Digital Ocean** as the cloud provider. The focus is on deploying the **Local AI Starter Kit by n8n**, but the steps are adaptable for deploying various localhost applications. The process encompasses setting up a cloud server, configuring necessary services, securing the application, and running it using Docker. Below is a comprehensive summary, including related resources, step-by-step instructions, and relevant code snippets.

---

#### **Table of Contents**

1. Overview
2. Prerequisites
3. Step 1: Setting Up a Digital Ocean Droplet
4. Step 2: Cloning the Git Repository
5. Step 3: Configuring Environment Variables
6. Step 4: Editing the [[Docker]] Compose File
7. Step 5: Setting Up the Firewall
8. Step 6: Installing and Configuring Nginx
9. Step 7: Setting Up SSL with Certbot
10. Step 8: Running Docker Containers
11. Step 9: Configuring n8n Workflows
12. Additional Resources

---

### **Overview**

Deploying AI applications to the cloud transforms a local development environment into a production-ready setup accessible via the internet. This guide uses the **Local AI Starter Kit by n8n**, which integrates various services like **Ollama** for language models, **Quadrant** for vector databases, **PostgreSQL** for SQL databases, and **n8n** for workflow automation. The deployment process ensures that these services are securely accessible and scalable.

### **Prerequisites**

- **Digital Ocean Account**: [Sign Up](https://www.digitalocean.com/)
- **Git Installed**: [Git Installation Guide](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- **Basic Knowledge of Linux Commands**
- **Domain Name**: Managed via a DNS provider like Namecheap, Bluehost, or Squarespace.

### **Step 1: Setting Up a Digital Ocean Droplet**

1. **Log into Digital Ocean**: Navigate to your Digital Ocean Dashboard.
2. **Create a Droplet**:

    - Click on **"Create"** in the top right corner and select **"Droplet"**.
    - **Choose an Image**: Go to the **Marketplace** tab and select **"Docker for Ubuntu"**.
    - **Select Droplet Size**: Opt for the **Basic Plan** suitable for running smaller models.
    - **Choose a Data Center Region**: Select a region closest to your target users.
    - **Set Authentication**: Use a password or SSH keys for secure access.
    - **Finalize**: Optionally, set a hostname (e.g., `youtube-ai-app-deploy`).
    - Click **"Create Droplet"**.

3. **Access the Droplet**:

    - Once created, click on the **"Access"** button to launch the Droplet console.

### **Step 2: Cloning the Git Repository**

1. **Clone the Repository**:

    ```bash
    git clone <repository_url>
    ```

    Replace `<repository_url>` with the actual URL of the Local AI Starter Kit repository.

2. **Navigate to the Project Directory**:

    ```bash
    cd <repository_folder>
    ```

### **Step 3: Configuring Environment Variables**

1. **Edit the** `**.env**` **File**:

    ```bash
    nano .env
    ```

2. **Set Up Variables**:

    - **PostgreSQL Credentials**:

        ```bash
        POSTGRES_USER=root
        POSTGRES_PASSWORD=password
        POSTGRES_DB=n8n
        ```

    - **n8n Security**:

        ```bash
        N8N_ENCRYPTION_KEY=your_encryption_key
        N8N_BASIC_AUTH_ACTIVE=true
        N8N_BASIC_AUTH_USER=your_username
        N8N_BASIC_AUTH_PASSWORD=your_password
        ```

        > **Note**: Replace placeholders with secure values.

3. **Save and Exit**:

    - Press `Ctrl + X`, then `Y`, and `Enter` to save changes.

4. **Verify Changes**:

    ```bash
    cat .env
    ```

### **Step 4: Editing the Docker Compose File**

1. **Open** `**docker-compose.yml**`:

    ```bash
    nano docker-compose.yml
    ```

2. **Modify Services**:

    - **[[Ollama]] Service**: Add the desired models. For example:

        ```bash
        ollama:
          image: ollama/ollama:latest
          command: ["ollama", "run", "llama-3.2", "embeddings"]
        ```

    - Ensure all necessary models are pulled at startup to avoid runtime delays.

3. **Save and Exit**:

    - Press `Ctrl + X`, then `Y`, and `Enter`.

### **Step 5: Setting Up the Firewall**

1. **Enable UFW (Uncomplicated Firewall)**:

    ```bash
    sudo ufw enable
    ```

2. **Allow Necessary Ports**:

    ```bash
    sudo ufw allow 80/tcp
    sudo ufw allow 443/tcp
    ```

3. **Reload UFW to Apply Rules**:

    ```bash
    sudo ufw reload
    ```

4. **Verify UFW Status**:

    ```bash
    sudo ufw status
    ```

### **Step 6: Installing and Configuring Nginx**

1. **Install Nginx**:

    ```bash
    sudo apt update
    sudo apt install nginx -y
    ```

2. **Configure Nginx as a Reverse Proxy**:

    - **Create a New Configuration File**:

        ```bash
        sudo nano /etc/nginx/sites-available/n8n.conf
        ```

    - **Add the Following Configuration**:

        ```bash
        server {
            listen 80;
            server_name yourdomain.com;
        
            location / {
                proxy_pass http://localhost:5678;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Forwarded-Proto $scheme;
            }
        }
        ```

        > **Replace** `yourdomain.com` with your actual domain or subdomain (e.g., `n8n.yourdomain.com`).

3. **Enable the Configuration**:

    ```bash
    sudo ln -s /etc/nginx/sites-available/n8n.conf /etc/nginx/sites-enabled/
    ```

4. **Test Nginx Configuration**:

    ```bash
    sudo nginx -t
    ```

    - Ensure there are no syntax errors.

5. **Reload Nginx**:

    ```bash
    sudo systemctl reload nginx
    ```

### **Step 7: Setting Up SSL with Certbot**

1. **Install Certbot**:

    ```bash
    sudo apt install certbot python3-certbot-nginx -y
    ```

2. **Obtain an SSL Certificate**:

    ```bash
    sudo certbot --nginx -d yourdomain.com
    ```

    - Follow the interactive prompts:
        - Enter your email.
        - Agree to terms and conditions.
        - Choose to redirect HTTP traffic to HTTPS.

3. **Verify SSL Installation**:

    - Access `https://yourdomain.com` in your browser.
    - Ensure the connection is secure (no warnings).

4. **Automate Certificate Renewal**:

    - Certbot sets up automatic renewal. To test, run:

        ```bash
        sudo certbot renew --dry-run
        ```

### **Step 8: Running [[Docker]] Containers**

1. **Navigate to the Project Directory**:

    ```bash
    cd <repository_folder>
    ```

2. **Run Docker Compose**:

    ```bash
    docker-compose up -d
    ```

    - **Options**:
        - `-d`: Runs containers in detached mode.
        - **GPU Support**: If using a GPU, refer to the repository's README for specific instructions.

3. **Monitor Logs**:

    ```bash
    docker-compose logs -f
    ```

    - Use `Ctrl + C` to exit log monitoring.

4. **Manage Containers**:

    - **Stop Containers**:

        ```bash
        docker-compose down
        ```

    - **View Logs**:

        ```bash
        docker-compose logs
        ```

### **Step 9: Configuring n8n Workflows**

1. **Access n8n**:

    - Navigate to `https://yourdomain.com` in your browser.
    - **Set Up n8n Account**: Create an account as prompted.

2. **Import Existing Workflow**:

    - Import workflows from previous setups or create new ones.

3. **Configure Service Connections**:

    - **Ollama**:
        - **Base URL**: `http://ollama:11434`
        - **Port**: `11434`
    - **PostgreSQL**:
        - **Host**: `postgresql`
        - **Database**: `n8n`
        - **User**: `root`
        - **Password**: `password`
    - **Quadrant**:
        - **API Key**: Any secure key.
        - **URL**: `http://quadrant:6333`
        - **Port**: `6333`

4. **Test the Setup**:

    - Send a test request (e.g., a chat message) to ensure all connections are functioning correctly.

---

### **Additional Resources**

- **Digital Ocean Documentation**:
    - Droplet Creation
    - Managing DNS
- **n8n Documentation**:
    - [Local AI Starter Kit](https://github.com/n8n-io/local-ai-starter)
- **Docker Documentation**:
    - Docker Compose
- **Nginx Documentation**:
    - Nginx Reverse Proxy
- **Certbot Documentation**:
    - Certbot Nginx Instructions
- **Runpod** (Alternative for GPU Instances):
    - [Runpod](https://runpod.io/) – Recommended for deploying applications requiring powerful GPUs.

---

### **Conclusion**

Deploying AI applications to the cloud involves several critical steps to ensure accessibility, security, and scalability. By following this guide, you can transform your local AI projects into robust, cloud-based applications accessible to users worldwide. Whether you're deploying the n8n Local AI Starter Kit or other localhost applications like Streamlit or Next.js, the outlined steps provide a solid foundation for successful deployment.

If you encounter any issues or have questions about specific steps, feel free to leave a comment or reach out for assistance.

   [[Workflow]]   [[AI Agents]]   [[Cloud]]