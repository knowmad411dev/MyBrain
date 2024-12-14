---
tags:
- home
video-url: https://www.youtube.com/watch?v=Ojo80oFQte8&list=WL&index=2
---
### Overview of AI Server

This document provides a detailed breakdown of the **AI Server** mentioned in the video, including information about the [[GitHub]] repository, installation instructions, hardware suggestions, and code examples for integration. **AI Server** is a free, self-hosted, unified API that allows users to interact with a wide variety of AI models and services, providing control over how these interactions are managed by self-hosting. Here is a detailed overview of the AI Server, its features, and how you can set it up.

### GitHub Repository Location

The AI Server is hosted on GitHub at the following location:

- **GitHub Repository**: `server stack ai-server`

To begin, you need to **clone the AI server repository** to your local machine. You can do this by running the following command:

```bash
git clone https://github.com/server-stack/ai-server.git
```

### Installation Instructions

Once you have cloned the repository, follow these steps to set up the AI server:

1. **Change to the Directory**:
   Navigate to the AI Server directory you’ve cloned:
   ```bash
   cd ai-server
   ```

2. **Run Installation Script**:
   Use the provided `install.sh` script to set up the AI server:
   ```bash
   cat install.sh | bash
   ```

   This script acts as a friendly installer to guide you through the setup process. The script will:

   - Automatically detect common API keys (e.g., for services like **Anthropic**, **OpenRouter**, **Google Cloud**, **OpenAI**, etc.).
   - Allow you to provide API keys for various services including:
     - **Open Router**: Provides access to a wide range of language models (LLMs).
     - **OpenAI**: Useful for generating images and voice using sophisticated models.
     - **Replicate.com**: Acts as a media provider, enabling capabilities such as **text-to-image** generation using models like Flux Pro.

3. **Configuration Files**:
   - Once you have provided the necessary API keys, you will be prompted to create an **OAuth secret**. This secret is used to access the **AI server's admin UI**.
   - Configuration details, including API keys, are saved in a **`.env`** file. You can review and edit this file before starting the server.

4. **Start the Server**:
   The server will run by default on `localhost:5006`. To access the admin portal, visit:
   ```
   http://localhost:5006/admin
   ```

   You will need to use the **OAuth secret** you configured during installation.

### Features of AI Server

**AI Server** is a self-hosted solution designed to simplify interaction with various AI models and services through a unified API. Below is an overview of its key features and components:

1. **Unified API for Multiple AI Providers**:
   AI Server serves as a **single entry point** for interacting with multiple LLM integrations:
   - **Text to Image**: Using OpenAI, **Comfy UI Agent**, or **Replicate**.
   - **Image to Image**, **Image to Text**: Using configured agents like Comfy UI.
   - **Text to Speech**, **Speech to Text**: Utilizing providers such as **OpenAI Whisper**.

2. **Comfy UI Agent**:
   - The **Comfy UI agent** has been containerized for **ease of deployment**.
   - It can run on separate hosts and can be registered with your AI server to act as a **media provider**.

3. **Admin Portal**:
   - Provides a UI for managing **AI providers**, **API keys**, and monitoring **background tasks**.
   - Allows you to **generate API keys**, integrate with applications, and test the setup.

4. **API Client Support for Multiple Languages**:
   AI Server offers typed client support for **11 different programming languages**, including:
   - **Python**, **Java**, **Swift**, **PHP**, **C**, **TypeScript**, etc.
   - These clients provide **typed DTOs (Data Transfer Objects)** which can be reused directly with compatible services like **Ollama**.

### AI Server UI Walkthrough

AI Server includes a set of UIs for interacting with different AI models and services:

1. **Chat UI**:
   - **Purpose**: Used for testing configured AI providers.
   - **Features**: Dropdown to select AI model, system prompt configuration, history viewing on the right-hand side.

2. **Text to Image UI**:
   - Supports different media providers like **Comfy UI**, **Replicate.com**, and **OpenAI DALL-E**.
   - **Prompt Customization**: You can specify **positive and negative prompts**, **resolution**, **image size**, and **tags**.

3. **Image to Text UI**:
   - Uses **Comfy UI agent** and the **Florence 2 model** to generate textual descriptions of images.

4. **Image to Image UI**:
   - Capable of transforming existing images based on the provided prompt using **inpainting** techniques with an **XD XL model**.
   - **Denoising**: The level of denoising can be adjusted to determine how much the image changes.

5. **Image Upscaling**:
   - Doubles the size of existing images using **upscaling models** on your configured Comfy UI agent.

6. **Speech to Text**:
   - Uses **OpenAI's Whisper model** through the **Comfy UI agent** to convert audio files to text. This is useful for generating **subtitles**.

7. **Text to Speech**:
   - Converts text to audio using either your **Comfy UI agent** or **OpenAI voice models**.

### Hardware Requirements

**AI Server** benefits from specific hardware to run optimally, especially for resource-intensive tasks:

- **NVIDIA GPUs**: Recommended for running most of the AI models efficiently, including image processing and large language model inference.
- The **installation process** for the Comfy UI agent is designed to allow it to be installed on **separate hosts**, making it easier to run resource-heavy tasks without overloading your primary server.

**Comfy UI Agent Hardware Notes**:
- Installing the Comfy UI agent on separate hardware can help manage resource allocation more effectively. For example, a powerful GPU machine can be used for heavy workloads like image processing, while the main server handles lightweight requests.

### Running the AI Server

- The server runs on **localhost:5006**.
- You can use the **admin portal** (`http://localhost:5006/admin`) to:
  - Configure AI providers.
  - Generate and manage API keys.
  - Monitor background jobs and check the history of completed tasks.

### Code Examples & Integration

1. **Python Client Example**:
   Below is a sample Python script that shows how to interact with AI Server’s API:
   ```python
   import requests

   url = "http://localhost:5006/api/chat"
   headers = {
       "Authorization": "Bearer <your_token_here>",
       "Content-Type": "application/json"
   }
   data = {
       "model": "gpt-3.5",
       "messages": [
           {"role": "system", "content": "You are an assistant."},
           {"role": "user", "content": "Explain quantum computing."}
       ]
   }

   response = requests.post(url, headers=headers, json=data)

   if response.status_code == 200:
       print("Response:", response.json())
   else:
       print("Error:", response.status_code, response.text)
   ```

   This code example demonstrates the use of AI Server’s chat API to send a prompt to a model and receive a response.

2. **JavaScript Client Example** (Using TypeScript):
   TypeScript integration is also available to use AI Server in JavaScript applications. Below is an example:
   ```typescript
   import axios from 'axios';

   const API_URL = "http://localhost:5006/api/text-to-image";
   const token = "<your_token_here>";

   async function generateImage(prompt: string) {
       try {
           const response = await axios.post(API_URL, {
               prompt: prompt,
               resolution: "1024x1024"
           }, {
               headers: {
                   'Authorization': `Bearer ${token}`,
                   'Content-Type': 'application/json'
               }
           });

           console.log('Generated Image URL:', response.data.image_url);
       } catch (error) {
           console.error('Error generating image:', error);
       }
   }

   generateImage("A futuristic cityscape during sunset");
   ```

### Additional Resources and Documentation

- **GitHub Repository**: Documentation, examples, and installation instructions are available on GitHub (`server stack ai-server`).
- **Admin UI**: Explore the configuration and management options via the admin UI running on **localhost:5006/admin**.
- **Official Documentation**: Documentation includes detailed examples and in-depth descriptions of each API.

### Summary

- **AI Server** is a unified self-hosted API server for interacting with a wide variety of **LLMs** and **AI services**.
- **Key Components**:
  - **Comfy UI Agent**: Provides support for image generation, upscaling, and other media tasks.
  - **OAuth Security**: Allows secure access to the **admin UI**.
  - **Typed Client Support**: Available for multiple languages, which makes integration with applications straightforward.
- **Installation** is straightforward with an **install script**, and API keys are managed through a `.env` file.
- **Hardware**: **NVIDIA GPUs** are recommended for optimal performance, particularly for image and model-based processing tasks.

This setup is suitable for developers looking for a self-hosted alternative that combines flexibility and control with a range of AI model integrations. With AI Server, you can create a powerful unified API to interact with AI models, self-hosted on your own infrastructure.

[[ML Hardware]]  [[Home]]  [[Python]]  