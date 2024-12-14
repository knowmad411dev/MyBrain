---
tags:
- obsidian
- llm
video-url: https://www.youtube.com/watch?v=7OcwwYtKsec&list=WL&index=2
---
## **BEST Local LLMs for Obsidian AI With LM Studio

### Overview of Stable LM2 Model Setup and Usage in LM Studio

This tutorial by Mike provides an in-depth overview of using Stable LM2, a local AI model designed to run efficiently on modern machines with limited RAM or GPU power. Below, you'll find a detailed step-by-step guide that covers everything from downloading and installing the LM Studio to selecting the most suitable model for your setup.

#### Minimum Requirements

**Hardware Requirements:**
- **Mac Users:** This only works on Apple silicon (M1, M2, M3). You need macOS 13.6 or newer.
- **PC (Windows/Linux) Users:** Your processor must support AVX2, and at least 16 GB of RAM is recommended. For GPU efficiency, 6 GB of VRAM or more is advised.

**Note:** Older Intel-based Macs are not supported.

#### Step-by-Step Guide to Downloading and Setting Up LM Studio

1. **Navigate to LM Studio's Website**:
   - On the website, you'll find three download links: Mac, Windows, and Linux.
   - Ensure you download the correct version for your operating system.

2. **Install LM Studio**:
   - Follow the installation process for your respective OS.
   - If you've used LM Studio previously, it's worth noting that the latest version comes with enhanced features, including an improved search page.

3. **Search for Stable LM2**:
   - After installation, open LM Studio.
   - Use the search bar to find the model by typing `stable lm2` (without spaces).
   - Hit **Enter** or click **Go** to see the available models.

4. **Filter Search Results**:
   - To ensure compatibility, filter the results by selecting "Most Likes" and "Compatibility".
   - This helps guarantee that the model you download will run smoothly on your setup.

#### Choosing the Right Quantization Level

Quantization affects the model's performance, file size, and quality:

- **Higher Quantization Levels** (e.g., Q4, Q8): Better quality but larger file sizes.
- **Lower Quantization Levels** (e.g., Q2): Smaller files but significant loss in quality.
- **Recommendation**: If you have sufficient RAM (16 GB or more), select **Q8** for the best balance of performance and quality. For those with less memory, **Q4** might be a better fit.

#### Downloading the Model

1. **Stable LM2 Model**:
   - From the filtered results, select the version that fits your system's capability. For instance, the **Q8** version is about 1.75 GB in size.
   - Users with Apple Silicon Macs and 16 GB RAM can comfortably use the **1.75 GB Q8** model.

2. **Neural Beagle Model**:
   - To download another model, type `neural beagle` in the search bar.
   - Choose the model by **M Labone** and look for the one with full GPU offload compatibility.
   - Ensure to select a version that works best with your RAM and GPU configuration.

3. **Dolphin 7B DPO Laser Model** (Uncensored Version):
   - Type `Dolphin 7B DPO laser` in the search bar.
   - Select the model posted by **The Bloke**, and scroll down to download the best available version for your hardware.

#### Managing the Downloaded Models

- After downloading the models, navigate to the folder where they're stored.
- You should see three separate versions for the different models:
  1. **Stable LM2**: Select the **Zephyr preset**.
  2. **Neural Beagle and Dolphin Models**: Use the **Chat ML** setting, as it generally works well with these models.

#### Testing the Models

Once the models are downloaded and configured:

- **Stable LM2**: Type in the search bar (e.g., "What is the Obsidian note-taking app?") and interact with the model.
- Testing results may vary based on your hardware, quantization level, and RAM availability.

**Note:** If your GPU offload says "may be possible," the model might partially run on your GPU, potentially speeding up inference. However, if it says "likely too large," the model will probably not work well on your system.

#### Tips for Optimizing Performance

- **Full GPU Offload**: If possible, always aim for a model that supports full GPU offload for smoother operation.
- **Quantization Trade-offs**: Higher quantization models (e.g., **Q8**) preserve more quality and are better suited if you have enough resources. Lower quantized models (e.g., **Q2**) reduce quality but also reduce the file size, making them feasible for systems with less RAM or GPU capability.
- **RAM Considerations**: For **7 billion parameter models**, at least 16 GB of RAM is ideal.

#### Running LM Studio Interactions

- Click the chat icon in LM Studio to interact with the selected model.
- Start by typing questions or prompts, such as "What is Obsidian?" to see how well the model responds.
- This helps you assess the model's knowledge, inference quality, and overall performance.

#### Wrap-Up and Future Testing

This guide helps you get started with Stable LM2 and other local models using LM Studio. If you plan to continue exploring local LLMs, make sure to:

- Test each model thoroughly to find the one that suits your use case best.
- Stay updated with future releases like **Mistol** and **Llama 3**, which promise to push the boundaries of open-source LLM capabilities.

Mike ends his tutorial by reminding viewers to ask questions and suggests that further testing of all the models will be covered in upcoming videos. Stay tuned for more updates and tests regarding the performance of different models.

[[Obsidian]]  [[LLM]] 