---
tags:
- agents
- machine-learning
- python
---

## **Video on NVIDIA NeMo (NVIDIA NEMs)**

This summary provides an overview of NVIDIA NeMo (Neural Modules), a toolkit for building AI applications without the need for extensive local hardware resources. NVIDIA NeMo simplifies the deployment of AI models at scale, offering developers pre-built models and pipelines that can be used both via cloud services and locally if the hardware permits.

---

## Introduction to NVIDIA NeMo

NVIDIA NeMo is a toolkit designed to simplify the development and deployment of AI applications, particularly in the realm of conversational AI and language models. It provides access to a catalog of pre-trained models and agents that can be integrated into applications without the need for significant local computational resources.

## NeMo Models and Agents

### NeMo Models

NeMo offers a variety of pre-trained models, including large language models like LLaMA 2. Developers can select models from the [NeMo Model Catalog](https://catalog.ngc.nvidia.com/models), which currently includes:

- **LLaMA 2 (40B)**: A 40-billion-parameter model that excels in language understanding and generation tasks.
- **SDXL**: A state-of-the-art text-to-image model.
- **Other specialized models**: For tasks like speech recognition, text-to-speech, and more.

### NeMo Agents

NeMo Agents are optimized pipelines that connect multiple models to perform complex tasks. Examples include:

- **Multimodal PDF Extraction**: Extract text and images from PDF documents.
- **Digital Human Interaction**: Create interactive digital avatars that can engage in conversation.
- **Small Molecule Development**: Assist in the development of pharmaceutical compounds.

## Using NeMo via API in Python

### Prerequisites

- **Python 3.6+**
- **OpenAI Python Library**: Install using `pip install openai`

### Steps

**1. Sign Up and Obtain API Key**

- Visit the [NVIDIA NeMo Service](https://nvidia.com/nemo) and sign up using your email or preferred login method.
- Generate an API key from your account dashboard.

**2. Set Up the Python Environment**

Create a new project directory and set up a virtual environment:

```bash
mkdir test_nemo
cd test_nemo
python -m venv venv
```

Activate the virtual environment:

- On macOS/Linux:

    ```bash
    source venv/bin/activate
    ```

- On Windows:

    ```bash
    venv\Scripts\activate
    ```

Install the OpenAI Python library:

```bash
pip install openai
```

**3. Sample Code to Use a NeMo Model**

Create a new Python script `test.py` with the following content:

```python
import os
import openai

# Set up your API key
openai.api_key = "YOUR_NEMO_API_KEY"

# Specify the API base and version
openai.api_base = "https://your_nvidia_nemo_endpoint/v1"
openai.api_type = "nvidia_chat"
openai.api_version = "2023-07-01"

# Define the model deployment name
deployment_name = "llama-2-70b-chat"

# Create a chat completion request
response = openai.ChatCompletion.create(
    engine=deployment_name,
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "Tell me about Dumbledore."}
    ]
)

# Print the assistant's reply
print(response['choices'][0]['message']['content'])
```

**4. Run the Script**

Execute the script in your terminal:

```bash
python test.py
```

This script sends a prompt to the NeMo model and prints the response.

## Customizing Models with LoRA

### What is LoRA?

[LoRA (Low-Rank Adaptation)](https://arxiv.org/abs/2106.09685) is a technique for fine-tuning large language models efficiently by adjusting a smaller number of parameters.

### How to Fine-Tune NeMo Models with LoRA

**1. Prepare Training Data**

Collect and format your dataset according to the model's requirements.

**2. Use NeMo's Fine-Tuning Tools**

NVIDIA provides tools for applying LoRA to their models. Follow tutorials such as [Fine-Tuning LLaMA 2 with LoRA](https://developer.nvidia.com/blog/fine-tune-llama-2-with-lora/) for detailed instructions.

**3. Deploy the Fine-Tuned Model**

After fine-tuning, deploy your custom model using NeMo's services or run it locally if hardware permits.

## Running NeMo Models Locally

### Requirements

- **High-End NVIDIA GPU**: Models like LLaMA 2 (40B) require significant VRAM.
- **Docker Installed**: To run NeMo containers.

### Steps

**1. Join NVIDIA Developer Program**

Sign up at the [NVIDIA Developer Program](https://developer.nvidia.com/).

**2. Install Docker and NVIDIA Container Toolkit**

- Install Docker: Docker Installation Guide
- Install NVIDIA Container Toolkit: [Installation Instructions](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html)

**3. Pull the NeMo Docker Container**

Log in to the NVIDIA container registry and pull the NeMo image:

```bash
docker login nvcr.io
docker pull nvcr.io/nvidia/nemo:latest
```

**4. Run the Container**

```
docker run --gpus all -it nvcr.io/nvidia/nemo:latest
```

**5. Check Compatibility**

Use the following command to verify if your hardware supports the desired model:

```bash
nemo_launcher --list-models --list-profiles
```

### Note

- Running large models locally requires substantial GPU memory (VRAM).
- If your hardware is insufficient, consider using NeMo's cloud services.

## Setting Up NeMo with Docker and WSL2

### Prerequisites

- **Windows 10/11 with WSL2 Enabled**
- **Docker Desktop Installed**

### Steps

**1. Enable WSL2 Backend in Docker Desktop**

Go to Docker Desktop settings and ensure WSL2 is enabled.

**2. Install NVIDIA Drivers for WSL2**

Download and install from [NVIDIA Drivers for CUDA on WSL](https://developer.nvidia.com/cuda/wsl).

**3. Install NVIDIA Container Toolkit**

Inside your WSL2 environment, execute the following commands:

```bash
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
sudo apt-get update
sudo apt-get install -y nvidia-docker2
```

**4. Configure Docker Daemon**

Edit Docker's daemon configuration to include the NVIDIA runtime. In your Docker settings (usually under Docker Engine), modify the JSON configuration:

```json
{
  "runtimes": {
    "nvidia": {
      "path": "nvidia-container-runtime",
      "runtimeArgs": []
    }
  },
  "default-runtime": "nvidia"
}
```

Apply changes and restart Docker.

**5. Run NeMo Container**

```bash
docker run --gpus all -it nvcr.io/nvidia/nemo:latest
```

### Troubleshooting

- **Insufficient VRAM**: If you encounter errors about low GPU memory, you may need a more powerful GPU.
- **WSL2 Limitations**: Some features may not work as expected in WSL2 compared to a native Linux environment.

## Conclusion

NVIDIA NeMo provides a powerful platform for developers to build and deploy AI applications efficiently. With access to large pre-trained models and the ability to customize them using techniques like LoRA, NeMo simplifies the AI development process. Whether you choose to use their cloud services or run models locally, NeMo offers flexibility to suit various development needs.

## Related URLs

- **NVIDIA NeMo Service**: [https://developer.nvidia.com/nvidia-nemo](https://developer.nvidia.com/nvidia-nemo)
- **NeMo Model Catalog**: [https://catalog.ngc.nvidia.com/models](https://catalog.ngc.nvidia.com/models)
- **NeMo Documentation**: [https://docs.nvidia.com/deeplearning/nemo/user-guide/docs/en/stable/](https://docs.nvidia.com/deeplearning/nemo/user-guide/docs/en/stable/)
- **Fine-Tuning with LoRA**: [https://developer.nvidia.com/blog/fine-tune-llama-2-with-lora/](https://developer.nvidia.com/blog/fine-tune-llama-2-with-lora/)
- **NVIDIA Developer Program**: [https://developer.nvidia.com/](https://developer.nvidia.com/)
- **Docker Installation Guide**: [https://docs.docker.com/get-docker/](https://docs.docker.com/get-docker/)
- **NVIDIA Container Toolkit Installation**: [https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html)
- **CUDA on WSL**: [https://developer.nvidia.com/cuda/wsl](https://developer.nvidia.com/cuda/wsl)

 [[Python]]  [[Docker]]  [[Machine learning]]