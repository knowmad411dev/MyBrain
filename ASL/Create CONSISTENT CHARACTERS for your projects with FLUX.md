---
tags:
- agents
- avatars
video-url: https://www.youtube.com/watch?v=MbQv8zoNEfY&list=WL&index=3
---
## **Create CONSISTENT CHARACTERS for your projects with FLUX

### **Overview**

The text discusses how to create consistent characters using a new workflow that leverages AI models like Flux, Stable Diffusion XL (SDXL), and Stable Diffusion 1.5. This workflow is useful for making cinematic movies, children's books, and AI influencers, focusing on consistency across multiple shots. A new AI image model called Flux has been integrated into the workflow to achieve better results.

The author explains how to:

1. Create a character sheet that represents characters from multiple angles and with different emotions.
2. Use a step-by-step automated workflow on Comi (a GUI for Stable Diffusion-related tools) to streamline the process.
3. Utilize training tools like Flux Gym to train personalized models called "Loras" for character consistency across generated images.
4. Implement techniques to enhance character appearance quality with upscaling, image noise, and film grain.

### **Step-by-Step Workflow Setup**

#### **1. Setting Up Comi and Flux**

- **Tools Needed**: You’ll need to install Comi, Flux, Stable Diffusion models, and a tool called Flux Gym.
- **Comi Workflow**: A four-step automated workflow was created for Comi, which can be installed via a provided guide.
- **Deactivate Steps**: In the beginning, deactivate all except the first group. Focus on importing the pose sheet and loading the correct models.

#### **2. Creating the Character Sheet**

- **Generate a Character Sheet**:
  - A **pose sheet** is generated, showing the character's basic skeletal pose in an OpenPose format.
  - **Import Pose Sheet**: Import the pose sheet into the workflow for character generation.
  - **Prompt**: Use a format like "character for fashion magazine, autumn fashion, brunette, gray coat" for character description.
  - **Adjust Prompts and Seeds**: If the generated image isn't perfect, tweak the seed value or prompt to get better results.

#### **3. Automate Character Workflow in Comi**

- **Groups to Activate**:
  - **First Group**: Adjust prompts and import the pose sheet. Add a name if needed.
  - **Second Group**: **Upscale** the initial character sheet for improved detail. This will refine the basic features.
  - **Third Group**: Extract **individual poses** for saving as separate images.
  - **Fourth Group**: Create **different emotions**. You can adjust sliders for expressions or rotate head poses for different perspectives.
- **Patreon Advanced Version**: The advanced version includes enhanced quality through upscaling individual face images, which helps with consistency when generating emotions for characters.

#### **4. Training a Lora**

- **What is a Lora?**:
  - Lora (short for Low-Rank Adaptation) helps add context to the AI model for the character being generated, making it easier to get consistent results.
  - **Create Dataset**:
    - Gather **10-15 high-quality images** of your character with different angles, emotions, and poses.
    - Use software like **Paint** to crop specific views if needed.
  - **Tool for Training**:
    - **Flux Gym**: A web UI specifically for training Loras.
    - Install via **Pinocchio** (a tool for one-click installs). Search for "Flux Gym" in the discover tab.
    - **Upload Images**: Drag and drop the dataset into Flux Gym.
    - **Tagging/Captions**: Either manually tag images (e.g., "gray background, smiling") or use **Florence 2** to automatically tag.
- **Training Setup**:
  - Specify a name for the Lora and choose the model to train on.
  - If you have more than 20 GB VRAM, training will be faster. Training with 12 GB VRAM will also work but slower.
  - Start training and let it download the required models. It could take around 30-40 minutes depending on system specifications.
- **Using Loras in Workflow**:
  - After training, save the Lora model and import it into the Comi workflow.
  - Set Lora strength to around 0.9-1 to generate consistent character features while retaining some freedom for new poses.
  - **Upscale and Film Grain**:
    - Add **upscaling** for more polished results.
    - Apply **film grain** to give it an analog or cinematic style.

#### **5. Enhancements and Troubleshooting**

- **Issues with Flux**:
  - Flux control may be slow, and results may sometimes be inconsistent, especially with stylized characters like anime or pixel art.
  - Consider using **SDXL control** for more robust results, or switch to SDXL workflow for a faster, more consistent process.
- **Using Multiple Characters**:
  - Load multiple Loras and reduce the strength slightly to avoid mixing styles.
  - Provide explicit descriptions for each character, including their position (e.g., "standing next to each other"), to prevent feature blending.

### **Workflow Variants**

- **Basic vs Advanced Workflow**:
  - The **basic workflow** involves generating a character sheet, saving individual poses, and extracting emotions.
  - The **advanced workflow** (available to Patreon supporters) adds features like upscaling of faces and individual body parts, as well as better integration for stylized characters.
- **Workflow Adjustments**:
  - For certain cases where character features don’t fit typical human anatomy (e.g., lizard people), extracting emotions may fail, but different angles will still be produced.
  - Use **SDXL Version** of the workflow for faster and more reliable outcomes, especially when trying to animate characters in other visual styles.

### **Tips for Successful Character Creation**

1. **Refine Prompts**: Continuously adjust the prompts and seed values to achieve desired characteristics.
2. **Adjust Lora Strength**: Lower the Lora strength to around 0.8 for some freedom in creation while retaining the overall style.
3. **Multiple Runs**: It may require several runs to get the right consistency and angles.
4. **Training Data Quality**: High-quality and varied training images (10-15 images from different perspectives) yield better Lora results.

### **Final Touches and Sharing**

- After generating character sheets, emotions, and final upscaled images, you can use them to **train an AI influencer** or **develop consistent illustrations for books**.
- Advanced users can take advantage of unique tricks like adding **noise during image generation** or using **film grain** for an authentic texture.

---

### **Key Takeaways**

- **Flux and SDXL** offer the ability to create consistent character appearances across different images, perfect for animation, storyboarding, or illustration.
- **Training a Lora** involves collecting good-quality images, tagging them appropriately, and using tools like Flux Gym.
- **Use Comi Workflow** to automate most of the image generation process, saving time while ensuring high-quality output.
- The advanced workflow adds significant value with **upscaling** and **enhanced quality adjustments**.

This workflow provides a comprehensive way to generate consistent characters, either for creative storytelling or branding, all through relatively accessible AI tools and techniques.

[[AI Agents]]  [[AI Avatars]]