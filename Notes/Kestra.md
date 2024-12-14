---
tags:
- automation
---

## **Kestra Workflow Product

### Overview of Kestra Unified Orchestration Platform

The video provides an overview of Kestra, a unified orchestration platform that helps simplify and govern business-critical workflows as code and via a UI. This platform is open-source and can be used as an alternative to tools like Zapier, Airflow, or Camunda. Here’s a detailed overview including how-to instructions and code.

#### Introduction to Kestra

- Kestra is an open-source orchestration tool used to build, schedule, and run workflows across various environments.
- It offers over 500 plugins and integrations, making it highly flexible for different tasks. It supports workflows coded in any language and allows users to manage them through a graphical interface.

#### Setting Up Kestra Locally with Docker

1. **Prerequisites**: Ensure that **Docker** is installed on your system. If not, visit the Docker website and follow installation instructions.
2. **Commands to Run**:

    - If you’re using **Mac/Linux**, use the command:

        ```
        docker run -d -p 8080:8080 kestra/kestra
        ```

    - For **Windows** users, use this command:

        ```
        docker run -d -p 8080:8080 kestra/kestra
        ```

    - After running the command, Docker will pull the image and set up Kestra locally.
    - Access the Kestra UI by navigating to `http://localhost:8080` in your browser.

3. **Running Kestra Locally**: Running this way is suitable for testing but doesn’t persist data after a container restart. To persist workflows, use the provided **Docker Compose** setup (more details below).

#### Self-Hosting Kestra with Coolify

1. **Set Up Coolify**:

    - Coolify is a free, open-source alternative to Vercel and can be used for managing self-hosted applications like Kestra.
    - To set up Coolify on a VPS, run:

        ```
        curl -sSL https://get.coolify.io | bash
        ```

2. **Create a New Project**:

    - Open Coolify, navigate to your projects, and create a new project for Kestra.
    - Add a **public repository** to host Kestra, and specify the GitHub repo URL (you may fork the Kestra repository for customization).
    - **Configuration**:
        - Change the build pack to **Docker Compose**.
        - Define environment variables, such as usernames and passwords, to set up Kestra securely.
        - Deploy Kestra by clicking on **Deploy** in Coolify.

#### Key Features of Kestra

1. **Dashboard**:

    - Provides an overview of workflow executions, success and fail ratios, and other key metrics.
    - Supports multiple namespaces to help organize workflows and view usage statistics.

2. **Blueprints**:

    - Kestra offers **Blueprints**, which are pre-configured templates to help users get started.
    - Examples of blueprints include S3 integration, SQL data handling, Slack notifications, and more.
    - You can filter Blueprints by tags and categories, which makes it easier to find relevant workflows.

3. **Plugins**:

    - Kestra has over **556 plugins** to integrate various tasks, triggers, and services like Slack, Git, Docker, and more.
    - The **plugin catalog** provides detailed documentation for setting up and using each plugin effectively.

4. **User Interface**:

    - **Topology View**: A visual representation of workflows, showing how tasks are interconnected.
    - **Editor**: Allows users to write workflow scripts directly in YAML. It also provides a side-by-side view with documentation to assist users in understanding syntax and configurations.

#### Creating and Running a Workflow in Kestra

1. **Define a Workflow**

    - Kestra workflows are written in YAML. Below is an example of a basic workflow that generates an SEO summary from a URL:

        ```
        id: generate_seo_summary
        namespace: company.team
        inputs:
          - name: article_url
            type: string
            default: "https://example.com/article"
        
        tasks:
          - id: fetch_article
            type: io.kestra.plugin.http.Download
            uri: "{{ inputs.article_url }}"
        
          - id: generate_seo_summary
            type: io.kestra.plugin.openai.ChatCompletion
            api_key: "YOUR_OPENAI_API_KEY"
            model: "gpt-3.5-turbo"
            max_tokens: 500
            prompt: |
              Write a short SEO-optimized summary for the following article: {{ outputs.fetch_article.content }}
        
          - id: log_output
            type: io.kestra.core.tasks.log.Log
            message: "Generated SEO Summary: {{ outputs.generate_seo_summary.choices[0].text }}"
        ```

2. **Running the Workflow**

    - After defining the workflow, it can be executed in Kestra's **Dashboard**.
    - Upon running, the workflow is displayed in **Gantt View** to visualize execution timing and dependencies.
    - Outputs can be logged or directed to other services like databases, emails, or Slack.

3. **Advanced Features**

    - **Namespace Management**: Organize workflows into namespaces for better separation.
    - **Concurrency and Dependencies**: Define concurrency limits and manage workflow dependencies using the built-in settings.

#### Summary of Key Concepts

- **Kestra Setup**: Kestra can be set up locally using Docker or hosted in production with Coolify.
- **Workflow Creation**: Workflows are defined using a YAML format, making them easy to version and manage.
- **Pre-Built Templates and Plugins**: Blueprints and plugins are available for various integrations and serve as a quick start for users.
- **Dashboard and Monitoring**: Kestra provides a comprehensive dashboard to manage workflow executions and view logs, metrics, and dependencies.

#### Additional Resources

- **GitHub Repository**: The original and forked repositories are available for customization.
- **Coolify Setup Video**: A full guide on setting up Coolify is also available on the YouTube channel.
- **Official Kestra Documentation**: To learn more, explore the Kestra documentation to understand advanced configurations and features.

[[Workflow]]