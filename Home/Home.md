---
tags: 
- home
---

## **Home

## **Overview of Smart Home Hardware Builds**

### 1. **Updated Custom Home Server Build**

This build is ideal if you need **maximum power and scalability**. It is designed to handle demanding AI workloads, dual GPUs, and can be future-proofed with additional upgrades. This setup is suited for those who plan to run large language models, complex computations, and require extensive processing power for smart home automation. However, it is costly and requires more space and power.

**Goal**: A powerful and scalable home server that can handle demanding AI workloads, support multiple GPUs, and provide seamless smart home automation.

**Components**:

1. **CPU**:

    - **Intel Core i9-13900K** or **AMD Ryzen 9 7950X**
        - Chosen for high performance to support multi-GPU configurations and handle concurrent processing tasks.

2. **Motherboard**:

    - **ASUS ROG Strix Z790-E Gaming WiFi** (for Intel) or **MSI MEG X670E ACE** (for AMD)
        - Supports dual-GPU setups, DDR5 RAM, and multiple PCIe 5.0 slots.
        - **Alternative**: **ASUS Pro WS WRX80E-SAGE SE** for even more GPU and RAM support.

3. **RAM**:

    - **Corsair Vengeance DDR5 64GB (2x32GB) 5600 MHz**
        - Provides ample memory for large datasets and multi-tasking.

4. **GPUs**:

    - **2 x NVIDIA RTX 4090 (24GB VRAM each)**
        - Delivers 48GB total VRAM for running large AI models, complex computations, and future-proofing for demanding tasks.
        - **Note**: SLI is not required for AI workloads.

5. **Primary Storage**:

    - **Samsung 980 PRO 2TB NVMe SSD**
        - Fast storage with sufficient space for datasets and models.

6. **Power Supply Unit (PSU)**:

    - **Corsair AX1600i 1600W 80+ Titanium Certified**
        - Capable of powering dual RTX 4090 GPUs and all other components.

7. **Case (Chassis)**:

    - **Fractal Design Define 7 XL**
        - Spacious design for easy installation and effective cooling with noise-dampening panels.

8. **Cooling System**:

    - **Corsair iCUE H150i Elite Liquid Cooler** (CPU)
    - **Case Fans**: **Noctua NF-A12x25** or **be quiet! Silent Wings 3** for optimal cooling.

9. **WiFi & Bluetooth Card**:

    - **TP-Link Archer TXE75E PCIe WiFi 6E & Bluetooth 5.2 Card**
        - Provides fast, modern wireless connectivity.

10. **Fast Network Card**:

    - **Intel X550-T2 10Gbps Ethernet Card**
        - High-speed wired networking for efficient data transfers.

11. **Operating System**:

    - **Ubuntu Server** or **Proxmox VE** for virtualization and advanced container management.

**Key Benefits**:

- **Massive GPU Power**: Dual RTX 4090s allow for running larger language models locally.
- **Scalable Design**: Built for future upgrades, from additional storage to extra network features.

### 2. **Custom Mini PC / Small Form Factor (SFF) Build**

This option provides a **compact and cost-effective solution** for running Home Assistant alongside moderate AI workloads. It balances performance and expandability in a smaller footprint, making it ideal for a more integrated smart home setup without the need for extreme computational power. This build is less costly and more practical if you don’t need the power of dual GPUs.

**Goal**: A compact yet powerful machine capable of running Home Assistant and AI workloads, balancing performance, size, and expandability.

**Components**:

1. **Processor (CPU)**:

    - **AMD Ryzen 7 7700X (8-Core, 16-Thread)**
        - Offers a good balance for Home Assistant and AI processing.
        - **Alternative**: **Intel Core i7-13700K** for higher single-threaded performance.

2. **GPU**:

    - **NVIDIA GeForce RTX 4070** (12GB VRAM)
        - Suitable for running AI models and even training small models locally.
        - **Alternative**: **RTX 3060** for more budget-friendly AI acceleration.

3. **Motherboard**:

    - **ASUS ROG Strix B650-I Gaming WiFi (Mini ITX)**
        - Compact form factor with WiFi 6E, PCIe 4.0, and M.2 slots for NVMe storage.

4. **RAM**:

    - **Corsair Vengeance DDR5 32GB (2x16GB) 5600MHz**
        - Adequate for Home Assistant and basic AI tasks; upgrade to **64GB** if workloads grow.

5. **Storage**:

    - **Samsung 980 Pro 1TB NVMe SSD**
        - Fast and efficient storage for models and datasets.

6. **Power Supply (PSU)**:

    - **Corsair SF750 Platinum SFX** (750W)
        - Sufficient power for the CPU, GPU, and future upgrades.

7. **Case**:

    - **Fractal Design Node 304** (Mini ITX)
        - Compact with good ventilation and support for a full-length GPU.
        - **Alternative**: **Cooler Master NR200** for better airflow.

8. **Cooling**:

    - **Noctua NH-L9a-AM5 Low-Profile CPU Cooler**
        - Low-profile design for compact cases with excellent cooling performance.

9. **Operating System & Software**:

    - **Ubuntu Linux 22.04 LTS** for lightweight and stable performance.
    - Run **Home Assistant** via **Docker** and utilize **NVIDIA Docker** for AI frameworks like **PyTorch** or **TensorFlow**.

10. **Network & Connectivity**:

    - **Sonoff Zigbee 3.0 USB Dongle Plus** or **Aeotec Z-Stick Gen5** for Zigbee/Z-Wave support to integrate smart devices.

**Key Considerations**:

- **Compatibility**: Ensure all components fit in the case.
- **Quiet Operation**: Noctua fans and good case ventilation help maintain quiet operation.
- **Software Setup**: Use Docker and Portainer to manage services easily.

**Estimated Cost**: **~$1,730**

### **Alternative Mini PC Options**

- **Beelink GTi Ultra with Dock**: A pre-built Mini PC that might provide sufficient performance for less demanding AI and automation tasks. Consider external GPU support for additional power.
    - **Link**: [Beelink GTi Ultra](https://www.amazon.com/Beelink-i9-12900H-Computer-Interaction-Fingerprint/dp/B0DD3XK4PR?sr=8-6&linkId=8ec75fe9c482798d6c4e9673ea240661&language=en_US&ref_=as_li_ss_tl)
    - **Dock**: [Beelink External Graphics Dock](https://www.amazon.com/Beelink-External-Graphics-Compatible-Discrete/dp/B0DFWNP7KX?sr=8-3&linkId=851ff2bb866fcaf9097c74f3be23165a&language=en_US&ref_=as_li_ss_tl)

### **Related Smart Home Topics**

- **[Home - Designing a Smart Home]**
- **[Home Assistant]**
- **[ESPHome]**
- **[Home Assistant & ESPHome Integration]**
- **[Home Sensors to AI]**
- **[Linux]**
- [[Windows]]