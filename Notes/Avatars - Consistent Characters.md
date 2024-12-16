---
tags:
- avatars
video-url: https://www.youtube.com/watch?v=MbQv8zoNEfY&list=WL&index=18
---

## Summary of the AI Character Workflow Video

This video covers **a detailed AI workflow to create consistent characters** using **Flux models** and **Stable Diffusion**. The process enables generating characters for projects such as **AI movies, children’s books, or influencers** while maintaining consistency across multiple images. Below is a structured breakdown of the video along with relevant **instructions, code, and tips**.

---

### **Challenges Addressed**

- Maintaining character consistency across images.
- Generating complex character traits (e.g., clothes, emotions, poses) with precision.
- Managing **multiple characters** in the same shot without style interference.

---

## **Steps and Tools for the Workflow**

### **1. Setting up the Workflow using Flux Model**

- **Models Used**:
    - **Flux**
    - **Stable Diffusion XL (SDXL)**
    - **Stable Diffusion 1.5**
- **Additional Interface**:
    - **Comi** (for automating steps)
    - **Pinokio installer** (for easy tool installation)

**Setup:**

1. Download and install **Comi** and the relevant models via the **Pinokio installer**.
2. Drag and drop the provided **workflow** file into Comi’s interface.
3. Ensure the necessary models (e.g., Flux) are loaded properly.
4. Import **character sheets** (with poses and emotions) to begin.

---

### **2. Generating a Character Sheet (Multiple Poses and Emotions)**

- **Create a pose sheet** depicting character angles and expressions.
- Use **Flux or SDXL models** to generate the character sheet based on provided prompts.
- Example **prompt for autumn fashion**:

```bash
Character: Fashion Model; Description: Autumn Clothing; Environment: Fashion Magazine Look.
```  
- **How to Adjust Image Quality**:
    - Change the **seed** if the result isn't satisfactory.
    - Use **Q Prompt** to generate new versions and fine-tune.

---

### **3. Working with the Workflow’s Groups**

- The workflow is divided into **groups** within Comi:
    - **Group 1**: Import the pose sheet and verify models.
    - **Group 2**: **Upscale** the character sheet to add more detail.
    - **Group 3**: Export **individual poses**.
    - **Group 4**: Add **different emotions and angles**.

**Customization:**

- Adjust **slider settings** to create varied expressions.
- Modify **rotation pitch** to get different face angles.

---

### **4. Troubleshooting and Faster Workflow (SDXL Alternative)**

- If **Flux is too slow**, switch to the **SDXL version**:
    - Use the **Wild Card Turbo Model** for speed.
    - Fine-tune **K-sampler settings** for consistency.
- Example: **Create Anime Characters** with SDXL in minutes.

---

### **5. Training a LoRA (Low-Rank Adaptation) Model**

- **What is a LoRA?**
    A technique to fine-tune AI models for specific characters by providing custom datasets.

#### **Steps to Train a LoRA:**

1. **Prepare a dataset**:
    - Select **10–15 images** with good quality, different angles, and emotions.
    - Example: Name the dataset **"Tina AI"**.
2. Use **Flux Gym UI** to train the LoRA:
    - Install Flux Gym via the **Pinokio installer**.
    - Set **trigger word** (e.g., "Tina AI") for easy use.
    - Drag and drop images into Flux Gym; either:
        - **Caption manually** (simpler descriptions preferred).
        - Use **Florence 2 tagging** for detailed descriptions.

**Training Process:**

- Select the **Flux Dev model** (if GPU > 20GB).
- Adjust model strength (0.9–1) for more control over outputs.
- Training can take **37 minutes or longer**, depending on the dataset size and hardware.

---

### **6. Using LoRA Models and Creating Final Characters**

- After training:
    - Save the **LoRA model** to the appropriate folder (e.g., Comi/models/luras).
    - Use the **Flux workflow** to apply the LoRA.
    - Adjust **noise levels** mid-generation for natural textures.

Example:

Generate the **Tina AI** character with a prompt like:

```bash
Tina AI, long red hair, wearing a brown turtleneck and gray coat, standing next to a wall.
```
---

### **7. Working with Multiple Characters**

- **Handling Style Interference**:
    - Load **multiple LoRA models**.
    - Reduce model **strength** slightly to give flexibility.
    - Use **character descriptions** to avoid hybridization. Example:

    ```baash
     Tina AI standing next to John AI, each looking towards the camera.
     ```   

---

### **Additional Tips and Resources**

- Use **upscaling tools** for improving pixel or anime-style characters.
- Film grain can be added to give images an **analog photography feel**.
- Consider **supporting the creator on Patreon** for advanced workflows, upscaling techniques, and exclusive datasets.

---

### **Links and Installation Guides**

- **Comi Installation**: Step-by-step instructions provided by the creator.
- **Pinokio Installer**: A user-friendly tool for downloading and setting up AI tools.
- **Flux Gym UI**: Easily train LoRA models with minimal setup.

---

This workflow is ideal for artists, storytellers, or anyone looking to generate consistent AI characters efficiently. It also emphasizes that **even imperfect results can be improved** through retries, fine-tuning, or using advanced tools.

[[AI Avatars]]