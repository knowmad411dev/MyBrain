---
tags: 
- machine-learning
- home
---

### Key Takeaways from "Building My Ultimate Machine Learning Rig from Scratch! | 2024 ML Software Setup Guide"

- **Purpose of the Build**:
    - Designed as a dedicated machine learning server to offload ML tasks from the creator's main computer.
    - Allows remote access for tasks like training jobs, running local LLMs, and generating Stable Diffusion outputs.
- **Hardware Highlights**:
    - **GPU**: NVIDIA GeForce RTX 480 Super (16 GB VRAM) for parallelizable ML tasks and LLMs.
    - **CPU**: Intel 14900K for handling data pre-processing and sequential ML tasks.
    - **RAM**: 96 GB GDDR5 to avoid disk access when VRAM is saturated.
    - **Storage**: 1 TB Samsung 980 Pro NVMe SSD for storing model weights and datasets.
    - **Motherboard**: Asus ROG STX Z790 I Gaming, supporting peak component performance.
    - **Cooling**: NZXT Kraken 280 AIO cooler with metrics display.
    - **Case**: Cooler Master NR200P V2, optimized for airflow with added fans.
    - **PSU**: Corsair 1,000 W FXL PSU with support for modern GPU power requirements.
- **Software Setup**:
    - **Operating System**: Ubuntu Server 22.04 LTS (Jammy Jellyfish) for stability and resource efficiency.
    - **Networking**: TailScale VPN for secure remote server access from any device.
    - **GPU Drivers**: NVIDIA drivers manually configured for optimal performance.
    - **ML Tools**:
        - **Ollama**: Easy LLM setup and management (e.g., Code Llama, Mixol).
        - **VS Code**: Browser-based Code-Server for programming anywhere on the TailScale network.
        - **PyTorch**: Installed with CUDA for GPU acceleration in ML projects.
        - **Docker**: For isolated container environments with GPU support (e.g., NVIDIA Isaac Gym for robot training).
- **ML Project Examples**:
    - Local deployment of text-to-video models like Anime Diffusion Lightning.
    - Experimentation with reinforcement learning tools (e.g., NVIDIA Isaac Gym).
    - Use of Hugging Face resources for open-source ML models.
- **Additional Notes**:
    - **TensorFlow Setup**: Installed with the CUDA toolkit and cuDNN for GPU acceleration.
    - **Versatility**: Docker containers configured for quick setup of ML environments.
    - **Challenges**: Importance of reading documentation and troubleshooting.
- **Main Takeaway**:
    - Building an ML rig requires attention to both hardware and software details, with persistence in addressing challenges.

[[Machine learning]] [[Home - Hardware]]