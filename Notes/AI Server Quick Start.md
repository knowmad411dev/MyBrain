---
tags:
- cloud
- home
---
## **AI Server Quick Start**

Install AI Server by running [install.sh](https://github.com/ServiceStack/ai-server/blob/main/install.sh):

### 1. Clone the Repository

Clone the AI Server repository from GitHub:

```bash
git clone https://github.com/ServiceStack/ai-server.git
```

### 2. Run the Installer

Navigate to the cloned repository and run the installer:

```bash
cd ai-server && cat install.sh | bash
```

The installer will detect common environment variables for its supported AI Providers, including OpenAI, Anthropic, Mistral AI, Google, etc., and will prompt you to include any others in your AI Server configuration.

```bash
~/projects/Demos$ cd ai-server/
~/projects/Demos/ai-server$ cat install.sh | bash
═══════════════════════════════════════════════════════════
            AI Provider Configuration            
═══════════════════════════════════════════════════════════
Found existing Anthropic Claude API key:
sk-ant-api...
┃  Use existing Anthropic Claude API key? ┃
┃                                          ┃
┃           Yes           No              ┃
←/→ toggle • enter submit • y Yes • n No
```

---

## Accessing AI Server

Once the AI Server is running, you can access the Admin Portal at [http://localhost:5006/admin](http://localhost:5006/admin) to configure your AI providers and generate API keys. If you first ran the AI Server with configured API Keys in your `.env` file, your providers will be automatically configured for the related services.

**INFO**: The default password to access the Admin Portal is `p@55wOrd`. You can change this in your `.env` file by setting the `AUTH_SECRET` or providing it during the installation process.

You will then be able to make requests to the AI Server API endpoints and access the Admin Portal user interface like the [Chat interface](http://localhost:5006/admin/Chat) to use your AI Provider models.

### Re-install

If needed, you can reset the process by deleting your local `App_Data` directory and rerunning `docker compose up` or re-running the `install.sh`.

### Optional - Install ComfyUI Agent

If your server also has a GPU, you can ask the installer to install the [ComfyUI Agent](https://docs.servicestack.net/ai-server/comfy-extension) locally:

```bash
Select which functionality you would like to support:
Use space to select, enter to confirm

Choose:
  ✓ Text & Image to Image (SDXL)
> ✓ Text to Image (Flux.Schnell)
  • Text to Image (SD 3.5)
  • Text to Speech (Piper)
  • Speech to Text (Whisper)
  • Image Upscale (RealESRGAN_x2)
  • Image to Text (Florence2)

x toggle • ↑ up • ↓ down • / filter • enter submit • ctrl+a select all
```

The ComfyUI Agent is a separate Docker agent for running [ComfyUI](https://www.comfy.org/), [Whisper](https://github.com/openai/whisper), and [FFmpeg](https://www.ffmpeg.org/) on servers with GPUs to handle AI Server's [Image](https://docs.servicestack.net/ai-server/transform/image) and [Video transformations](https://docs.servicestack.net/ai-server/transform/video) and Media Requests, including:

-   [Text to Image](https://docs.servicestack.net/ai-server/text-to-image)
-   [Image to Text](https://docs.servicestack.net/ai-server/image-to-text)
-   [Image to Image](https://docs.servicestack.net/ai-server/image-to-image)
-   [Image with Mask](https://docs.servicestack.net/ai-server/image-with-mask)
-   [Image Upscale](https://docs.servicestack.net/ai-server/image-upscale)
-   [Speech to Text](https://docs.servicestack.net/ai-server/speech-to-text)
-   [Text to Speech](https://docs.servicestack.net/ai-server/text-to-speech)

#### ComfyUI Agent Installer

To install the ComfyUI Agent on a separate server (with a GPU), clone and run the ComfyUI Agent installer from that server:

**Clone the Comfy Agent Repo:**

```bash
git clone https://github.com/ServiceStack/agent-comfy.git
```

**Run the Comfy Agent Installer:**

```bash
cd agent-comfy && cat install.sh | bash
```

Providing your AI Server URL and Auth Secret when prompted will automatically register the ComfyUI Agent with your AI Server to handle related requests.

You will be prompted to provide the AI Server URL and ComfyUI Agent URL during the installation. These should be the accessible URLs for your AI Server and ComfyUI Agent. When running locally, the ComfyUI Agent will be populated with a Docker-accessible path, as `localhost` won't be accessible from the AI Server container. If you want to reset the ComfyUI Agent settings, remember to remove the provider from the AI Server Admin Portal.

---

### Supported OS

The AI Server installer is supported on Linux, macOS, and Windows with WSL2, and all require Docker and Docker Compose to be installed at a minimum.

## Prerequisites

### [[Linux]]

Linux requires the following software installed:

-   [[Docker]] Engine (with Docker Compose)
-   [[Git]]

#### ComfyUI Agent

To run the ComfyUI Agent locally, you will also need:

-   Nvidia GPU with CUDA support
-   Nvidia Container Toolkit for [Docker](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html)

### macOS

macOS also requires:

-   Docker Engine (with Docker Compose)

#### ComfyUI Agent

ComfyUI Agent requires Pytorch running in Docker, which isn't available for macOS.

### [[Windows]] with WSL2

Windows with WSL2 requires the following prerequisites:

-   Docker Engine accessible from WSL2, like [Docker Desktop](https://www.docker.com/products/docker-desktop)
-   WSL2 with Ubuntu 20.04 LTS or later

#### ComfyUI Agent

To run the ComfyUI Agent locally, you will also need:

-   Nvidia GPU with [WSL2 CUDA support](https://docs.nvidia.com/cuda/wsl-user-guide/index.html)

---

[[ML Hardware]]  [[AI Server]]  [[Home]]