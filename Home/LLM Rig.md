---
tags:
- llm
- home
video-url: https://www.youtube.com/watch?v=IXixbu7Kkd8&list=WL&index=2
---

## **LLM Rig

This text details a hardware setup to run large language models (LLMs) locally, emphasizing the use of high-performance components and exploring how different systems handle GPU acceleration for AI workloads. Here's a structured breakdown of the various components and technologies mentioned:

### **1. Core Hardware Components:**

- **NVIDIA GeForce RTX 4090 GPU:**
  - A top-tier graphics card capable of handling high computational loads, particularly those required for running LLMs and GPU-accelerated tasks like AI modeling and graphics rendering. It comes with 24 GB of VRAM.
  - Notably, the RTX 4090 is referenced as being *overkill* for the application, but it's selected to test the efficiency of LLMs at higher speeds. The limitations of the 24 GB VRAM are discussed, particularly when attempting to run larger models that exceed this memory limit, necessitating quantization of models or using the CPU instead.
- **Minus Forum D1 with PCI Express Ulink 4i External GPU Adapter:**
  - **PCIe Ulink 4i External GPU Adapter:** Acts as an interface between the power supply, GPU, and the Mini PC, utilizing **Oculink** technology for connection. This is necessary because it allows the external GPU (the RTX 4090) to communicate with the Mini PC.
  - **Oculink Connectivity:** This technology allows speeds up to 63 Gbps, which is faster than the typical 40 Gbps limit of Thunderbolt 3/4 connections, giving the user a performance advantage. This is vital for effectively running an external GPU setup.
- **Minis Forum PC with Oculink Connection:**
  - A small form-factor Mini PC that serves as the main processing hub for this experiment. It connects to the external GPU via Oculink.
  - Emphasizes the trend of adding Oculink to compact PCs as a more efficient connection option compared to Thunderbolt.
- **Seic Vertex GX 1200W Power Supply:**
  - **1200W Power Supply:** Chosen as it provides ample power, potentially for future upgrades or additional components like dual RTX 4090s. It's overpowered for the current setup but selected with future expansion in mind.
  - The UPS (Uninterruptible Power Supply) struggles to handle the power spikes when using this powerful setup, indicating the high power demands of the RTX 4090.

### **2. Assembly Overview and Challenges:**

- The assembly includes connecting various power cables from the power supply to the GPU, the Oculink dock, and the Mini PC. Several challenges include:
  - **Cable Management:** The power supply includes a myriad of cables that must be properly connected, which is cumbersome given the over-sized power supply and the GPU requirements.
  - **Bracket for GPU Stability:** The large size of the GPU necessitates a bracket for stabilization as it won't stay upright by itself.
  - **Cooling Considerations:** The GPU's heat generation is discussed, and the absence of fan spin suggests that it wasn't under sufficient load to necessitate cooling initially.

### **3. Software and Setup:**

- **Operating System and Drivers:**
  - The system setup includes installing Windows, after which the GPU is recognized without additional drivers. Later, **Gigabyte drivers** for the RTX 4090 are downloaded to optimize the performance.
- **Development Environment Setup:**
  - **Python Installation:** Installed globally on the machine for running local scripts. The user prefers **Conda environments** for modular development, intending to set that up afterward.
  - **CUDA Toolkit Installation:** This toolkit is used to facilitate GPU acceleration for high-performance computing, essential for training or running LLMs. The toolkit allows for optimized GPU usage, especially critical when running large models.

### **4. Running LLMs Locally:**

- The user intends to run LLMs using the GPU to leverage the computational power of the RTX 4090. The following software and approaches are mentioned:
  - **AMA Tool for Running LLMs:** The AMA tool is used to interact with AI models locally. It's praised for its simplicity, and the setup appears to automatically detect the RTX 4090, utilizing it for inference without manual configuration.
  - **Model Testing:**
    - Smaller models (e.g., **Llama 3.1** with **4.7 GB size**) run smoothly, making full use of the GPU.
    - Larger models (e.g., **70 billion parameters**) require more VRAM than available on the RTX 4090, so the load is shifted to the CPU instead. This results in significantly slower processing, with high CPU usage, highlighting a key limitation of using the GPU for models that exceed the available VRAM.

### **5. Performance Observations:**

- The RTX 4090 was found to be significantly faster when running smaller AI models due to its powerful GPU capabilities.
- The setup's efficiency with **CUDA Z** showed performance metrics that exceeded Thunderbolt-based GPU connections, demonstrating the benefits of the faster **Oculink** technology.
- Despite using a high-end GPU, models that exceed the VRAM capacity still struggle, and the system has to revert to CPU processing, resulting in slower performance.

### **6. Additional Benchmarking Tools and Insights:**

- **Stable Diffusion Testing:** Used to generate images with text prompts, and the speed was noticeably impressive when utilizing the GPU.
- **Real-Time Response:** Testing showed the efficiency of the setup when running small to moderately sized models, with the GPU kicking in and the **UPS struggling** to keep up due to the increased power draw.
- **Fans and Cooling:** The GPU's fans only activate when under sufficient load, indicating efficient cooling, but it also means that under lower loads, the temperature can rise without activating the cooling mechanism.

### **Summary and Conclusion:**

- This setup combines a **Mini PC**, a **PCIe Oculink dock**, a **high-power PSU**, and an **RTX 4090** to create a compact yet highly capable platform for experimenting with LLMs locally.
- The Oculink connection provides significant speed advantages over Thunderbolt connections, which typically bottleneck at 40 Gbps.
- The RTX 4090's 24 GB of VRAM presents a limitation when running very large models, necessitating either model quantization or fallback to CPU processing.
- The hardware setup is overpowered for current needs but aims to provide flexibility for future expansion (e.g., possibly adding a second GPU).
- Overall, while the system is capable of handling LLMs efficiently up to a certain size, models that exceed the available VRAM require fallback strategies, such as CPU processing, which introduces latency and slower performance.

This build represents an experiment in maximizing computational efficiency for AI workloads using a compact form factor, and it showcases both the strengths and limitations of current GPU technology in local LLM use cases.

[[ML Hardware]]  [[LLM]]