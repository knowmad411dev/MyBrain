---
tags:
- llm
- home
---

## **Introduction to Local Machine Learning Models**

The speaker emphasizes the growing importance of running machine learning (ML) models locally to avoid long-term cloud computing costs. Running these models locally helps users maintain control over their infrastructure and reduce reliance on cloud-based services.

### **Hardware Overview for Local Model Deployment**

The video reviews various consumer hardware options for running ML models, ranging from compact devices to more powerful GPUs:

1. **Intel NUC-Style Box**: This device uses a Core Ultra 5 processor. A newer Series 2 processor is mentioned, which the speaker intends to test once available.
2. **Mac Mini with M2 Pro**: This hardware can run smaller models effectively and consumes less power than other devices.
3. **Mini PC with RTX 4090 GPU**: This system features an oculink-attached RTX 4090 GPU, allowing faster inference times but with constraints related to PCIe bandwidth.

These three devices represent a range of consumer-grade hardware but don't cover all possible ML hardware setups, such as the higher-end **Mac Studio with the M2 Ultra chip**, which has more memory.

### **Performance Considerations Across Devices**

The presenter compares the performance of the above hardware while running a **7 billion parameter LLaMA model**, taking into account various factors:

1. **Speed and Power Consumption**:
    - **Mac Mini M2 Pro**: Draws around 15 watts at idle and up to 57 watts under load. It has moderate speed and very low power consumption.
    - **Intel NUC-Style Box**: Shows slightly higher power consumption. Initially, it displayed power discrepancies that were later attributed to the monitor being connected via USB-C.
    - **RTX 4090 System**: Capable of high-speed performance with up to **320 watts** power consumption, significantly higher compared to other options.

The RTX 4090 system performs the fastest but has downsides related to its high power consumption and the need to transfer the model into VRAM, which is a bottleneck.

### **Speed and Efficiency Testing**:

The speaker uses a set of tests to evaluate efficiency, which include:

1. **Prompt Speed Test**: Each device is tested by generating a 1,000-word story.
    - The RTX 4090 outperformed other systems, but the Mac Mini was not far behind. The Intel NUC was slower as it used the CPU for generation.
2. **Wattage During Inference**:
    - The **Mac Mini** maintained relatively low power usage.
    - The **RTX 4090** drew the highest power but completed the task significantly faster.
    - The **Intel Machine** performed poorly in terms of speed and was also slower when running on the integrated GPU, despite lower wattage.

The presenter also mentioned efficiency metrics like **tokens per second**, comparing them across models ranging from 7 billion to 13 billion parameters. The **RTX 4090** showed very high throughput, comparable to commercial models like ChatGPT.

### **Cost, Heat, and Noise Considerations**:

**Power Consumption and Operational Cost**:

- The presenter calculates the **total energy consumption** for each device, factoring in power consumption over the entire generation process.
- The RTX 4090 is the fastest but has a higher overall energy cost.
- The **M2 Pro Mac Mini** is deemed the most energy-efficient in terms of cost per watt.

**Heat and Noise**:

- **Mac Mini**: Runs quietly with minimal heat, suitable for small workspaces.
- **Intel NUC**: Outputs more noticeable heat, though not as extreme as older Intel processors.
- **RTX 4090 System**: Produces the most heat and noise, requiring adequate cooling, especially in smaller environments.

**Cost of Ownership**:

- The presenter highlights costs such as initial hardware price and **operational electricity costs** based on energy prices in different regions (e.g., the United States vs. Germany or Denmark).
- They conclude that the **Mac Mini M2 Pro** is the most cost-effective solution overall, particularly when accounting for both initial costs and long-term energy use.

### **Summary and Personal Insights**:

The presenter provides their conclusions based on use cases:

1. **Best Performance for Long Runs**: The **RTX 4090** is ideal for scenarios needing the highest possible speed and throughput, especially when generating large text outputs.
2. **Fast Response Time**: The **Mac Mini M2 Pro** or the **Intel NUC** are better for applications requiring quick, short responses, like using an LLM as a coding assistant. The **RTX 4090** takes longer for the initial VRAM load, which makes it less ideal for short, frequent prompts.
3. **Noise, Heat, and Environment**: The **Mac Mini** offers the quietest and coolest operation, making it suitable for small office environments, while the **RTX 4090** is more challenging to manage in smaller, less ventilated spaces.

### **Considerations for Future Hardware**:

The presenter is interested in testing the **upcoming Intel Lunar Lake processors**, which promise improved efficiency, potentially offering an interesting alternative for ML enthusiasts seeking low-power devices.

### **Final Thoughts**:

- The **M2 Pro Mac Mini** strikes the best balance between cost, efficiency, and performance for a general-purpose machine learning workstation.
- The **RTX 4090**, although costly and power-hungry, provides unparalleled speed, especially for larger models and more computationally demanding tasks.
- The **Intel NUC**, while less efficient in this setting, could become more competitive with future upgrades, such as the Series 2 Lunar Lake.

Overall, the presentation offers a detailed evaluation of the three consumer-grade devices for running machine learning models, balancing factors like speed, power consumption, heat, noise, and cost, depending on specific user needs and preferences.

[[LLM]]  [[ML Hardware]]