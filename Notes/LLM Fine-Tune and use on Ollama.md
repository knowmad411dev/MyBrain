---
Video-URL: https://www.youtube.com/watch?v=pxhkDaKzBaY&list=WL&index=7
tags:
- ollama
- llm
---

## **[[LLM]] Fine-Tune and Use on [[Ollama]]**

### Comprehensive Guide to Fine-Tuning Large Language Models Locally with Ollama (oAMA)

Fine-tuning large language models (LLMs) allows you to customize AI behavior to suit specific tasks, such as generating SQL queries based on table data. This guide walks you through the process of fine-tuning an LLM locally using Ollama (oAMA), leveraging tools like Unsloth for efficient training and Chroma [[Vector Databases]] for managing embeddings. Whether you have a powerful GPU or are utilizing cloud resources like Google Colab, this guide covers all necessary steps, including how-to instructions, relevant links, and code snippets.

---

## Introduction

Fine-tuning large language models (LLMs) like **Llama 3.1** allows you to tailor AI capabilities to specific tasks, enhancing performance and relevance. By running these models locally with **Ollama (oAMA)**, you gain greater control, privacy, and efficiency. This guide demonstrates how to fine-tune an LLM to generate SQL queries based on table data using a dataset like **Synthetic Text-to-SQL**, leveraging tools like **Unsloth** for efficient training and **Chroma Vector Database** for managing embeddings.

## Prerequisites

Before proceeding, ensure you have the following:

### Hardware:

- **GPU Recommended**: Nvidia 4090 or similar for optimal performance.
- **CPU Only**: Possible but with significantly slower training times.

### Software:

- **Operating System**: Ubuntu (or compatible Linux distribution).
- **Anaconda**: For managing Python environments.
- **CUDA Libraries**: Version 12.1 recommended for GPU acceleration.
- **Python**: Version 3.10.
- **Docker**: For running Chroma Vector Database.
- **Git**: For cloning repositories.
- **Deno (Optional)**: For TypeScript implementations.

### Accounts:

- **Google Colab (Optional)**: If you don't have a local GPU, Google Colab can provide cloud-based GPU resources.

## Choosing the Right Dataset

Selecting an appropriate dataset is crucial for effective fine-tuning. A relevant dataset ensures that your model can perform the desired task efficiently. For generating SQL queries based on table data, the **Synthetic Text-to-SQL** dataset is ideal, containing over 105,000 records categorized into columns like prompt, SQL content, complexity, and more.

**Synthetic Text-to-SQL Dataset:**

- **Description**: Contains prompts and corresponding SQL queries to train models on SQL generation.
- **Link**: Synthetic Text-to-SQL Dataset (Replace with actual link if available)

## Setting Up the Environment

Proper environment setup is essential for seamless fine-tuning. Follow the steps below to configure your system.

### Installing Anaconda

**Anaconda** simplifies package management and deployment. Install it using the following steps:

1. **Download Anaconda**: Visit the [Anaconda Official Website](https://www.anaconda.com/) and download the installer for Ubuntu.
2. **Install Anaconda**:

    ```
    bash Anaconda3-2023.07-Linux-x86_64.sh
    ```

    Follow the on-screen prompts to complete the installation.

3. **Initialize Anaconda**:

    ```
    source ~/.bashrc
    ```

### Installing CUDA Libraries

**CUDA** is required for GPU acceleration during training.

1. **Download CUDA 12.1**: Visit the [NVIDIA CUDA Toolkit Download Page](https://developer.nvidia.com/cuda-downloads) and select CUDA 12.1 for your Ubuntu version.
2. **Install CUDA**:

    ```
    sudo dpkg -i cuda-repo-ubuntuXXXX_12.1.0-1_amd64.deb
    sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntuXXXX/x86_64/7fa2af80.pub
    sudo apt-get update
    sudo apt-get install cuda
    ```

3. **Verify CUDA Installation**:

    ```
    nvcc --version
    ```

    **Expected Output**:

    ```
    nvcc: NVIDIA (R) Cuda compiler driver
    Copyright (c) 2005-2023 NVIDIA Corporation
    Built on ...
    ```

### Installing Unsloth

**Unsloth** is a tool that facilitates efficient fine-tuning of open-source models with reduced memory usage.

1. **Create a New Conda Environment**:

    ```
    conda create -n unsloth_env python=3.10
    conda activate unsloth_env
    ```

2. **Install PyTorch with CUDA Support**:

    ```
    conda install pytorch torchvision torchaudio cudatoolkit=12.1 -c pytorch -c nvidia
    ```

3. **Install Unsloth**:

    ```
    pip install unsloth
    ```

4. **Install Jupyter Notebook (If Not Installed)**:

    ```
    pip install jupyter
    ```

5. **Launch Jupyter Notebook**:

    ```
    jupyter notebook
    ```

### Installing Jupyter

If you haven't installed **Jupyter** during the Unsloth installation, do so with:

```
conda install -c conda-forge notebook
```

## Fine-Tuning the Model with Unsloth

Fine-tuning involves training the LLM with your specific dataset to adapt its responses to your requirements.

### Preparing the Dataset

1. **Clone the Project Repository**:

    ```
    git clone https://github.com/technovangelist/videoprojects.git
    cd videoprojects/2024-09-10-buildrag
    ```

2. **Organize Your Scripts**: Ensure that your SQL generation scripts are stored in a directory, e.g., `scripts/`.

### Running the Fine-Tuning Process

1. **Create a Jupyter Notebook**:

    Open Jupyter Notebook from your terminal:

    ```
    jupyter notebook
    ```

    Create a new notebook named `fine_tune_unsloth.ipynb`.

2. **Import Required Libraries**:

    ```Python
    import unsloth
    from transformers import LlamaForCausalLM, LlamaTokenizer
    import torch
    ```

3. **Load the Llama 3.1 Model**:

    ```Python
    model_name = "llama-3.1-8bit"
    tokenizer = LlamaTokenizer.from_pretrained(model_name)
    model = LlamaForCausalLM.from_pretrained(
        model_name,
        load_in_8bit=True,
        device_map="auto"
    )
    ```

4. **Load PEFT (LoRA) Adapters**:

    ```Python
    from peft import get_peft_model, LoraConfig, TaskType
    
    peft_config = LoraConfig(
        task_type=TaskType.CAUSAL_LM,
        inference_mode=False,
        r=8,
        lora_alpha=16,
        lora_dropout=0.05,
        target_modules=["q_proj", "k_proj", "v_proj", "o_proj"]
    )
    
    model = get_peft_model(model, peft_config)
    ```

5. **Format the Dataset**:

    **Example Prompt Format (Alpaca Style)**:

    ```
    ### Instruction:
    Generate SQL based on the following table data.
    
    ### Input:
    Table Data: [Provide table data here]
    
    ### Response:
    [Generated SQL Query]
    ```

6. **Initialize the Trainer**:

    ```
    from unsloth import Trainer
    
    trainer = Trainer(
        model=model,
        train_dataset=train_dataset,  # Define your train_dataset
        eval_dataset=eval_dataset,    # Define your eval_dataset
        peft_config=peft_config,
        output_dir="./fine_tuned_model",
        per_device_train_batch_size=8,
        per_device_eval_batch_size=8,
        learning_rate=3e-4,
        num_train_epochs=3,
        logging_steps=10,
        save_steps=500,
        evaluation_strategy="steps",
        eval_steps=500,
        save_total_limit=2,
        load_best_model_at_end=True
    )
    ```

7. **Start Fine-Tuning**:

    ```
    trainer.train()
    ```

8. **Save the Fine-Tuned Model**:

    ```
    trainer.save_model()
    ```

9. **Convert the Model for Local Use**:

    ```
    unsloth convert --model_path ./fine_tuned_model --output_path ./fine_tuned_llama
    ```

10. **Verify the Fine-Tuned Model**:

    Use the following command to ensure the model is correctly fine-tuned:

    ```
    python run_model.py --model_path ./fine_tuned_llama --input "Generate SQL for the following table data."
    ```

---

## Importing and Managing Documents with Chroma

**Chroma Vector Database** is used to store and manage embeddings of document chunks, facilitating efficient retrieval during RAG.

### Setting Up Chroma Vector Database

1. **Run Chroma as a Docker Container**:

    ```
    docker run -d \
      -p 8000:8000 \
      -v chroma-data:/chromadb/data \
      chromadb/chroma
    ```

    **Parameters Explained**:

    - `-d`: Runs the container in detached mode.
    - `-p 8000:8000`: Maps port 8000 of the container to port 8000 on the host.
    - `-v chroma-data:/chromadb/data`: Mounts a Docker volume for persistent storage.
    - `chromadb/chroma`: Specifies the Chroma Docker image.

2. **Verify Chroma is Running**:

    Open your browser and navigate to `http://localhost:8000/docs` to access Chroma's API documentation.

---

## Conclusion

Fine-tuning large language models locally with **Ollama (oAMA)** empowers you to create highly specialized AI tools tailored to your specific needs, such as generating SQL queries from table data. By leveraging tools like **Unsloth** for efficient training and **Chroma Vector Database** for managing embeddings, you can build a robust **Retrieval-Augmented Generation (RAG)** system. Whether you prefer coding in Python or TypeScript, this guide provides the necessary steps, code snippets, and resources to get you started.

Key Takeaways:

RAG Enhances AI Models: Combines generative capabilities with real-time data retrieval for more accurate and up-to-date responses.

Efficient Fine-Tuning: Tools like Unsloth reduce memory usage and streamline the fine-tuning process.

Effective Document Management: Proper chunking and embedding of documents are crucial for effective retrieval in RAG systems.

Flexible Implementation: Choose between Python and TypeScript based on your preference or project requirements.

Leverage Pre-Built Tools: Tools like Open Web UI, MSTY, and Page Assist offer RAG functionalities without extensive coding.

Community and Support: Engage with the Ollama community and utilize

[[Ollama]]   [[LLM]]