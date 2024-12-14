---
Video-URL: https://www.youtube.com/watch?v=ez3EaqW1JyI
tags:
- python
---

## **[[Python]] Automating YouTube Video Creation with AI

In this guide, we'll explore how to create engaging YouTube videos using various AI tools. By automating scriptwriting, voiceovers, image generation, and video editing, you can save time and produce high-quality content efficiently.

---

## Introduction

Creating engaging YouTube content has traditionally involved significant time investment in scripting, voice recording, and video editing. However, with advancements in AI technology, it's now possible to automate much of this process. This guide demonstrates how to leverage AI tools to create a successful video channel, similar to a history and mythology channel that garnered 5.6 million views and generated up to $222,000 in 30 days.

---

## Step 1: Crafting the Script with SEO Writing AI

### Overview

Using **SEO Writing AI**, you can generate detailed scripts optimized for search engines. This tool allows you to create lengthy, engaging content tailored to specific keywords and settings.

### How-To Instructions

1. **Access SEO Writing AI:**

    - Navigate to the [SEO Writing AI](https://www.seowritingai.com) website.
    - Click on **"Get Started"**.
2. **Generate a Blog Post:**

    - Select **"OneClick Blog Post"**.
    - Enter your main keyword, e.g., `Zeus lovers`.
3. **Customize Settings:**

    - **Title:** _Exploring Greek Gods' Romantic Tales_
    - **Tone of Voice:** Witty
    - **Point of View:** Third person
    - **Target Country:** United States
    - **Article Size:** Medium (~3,000 words)
    - **AI Model:** GPT-4
    - **API Keys:** Ensure your API keys are included to reduce costs.
    - **Reading Level:** Keep it low for broader audience accessibility.
4. **Configure SEO Settings:**

    - **NLP Keywords Generation:** Enable to include relevant keywords for better ranking.
    - **Web Connection:** Use **Deep Web** to analyze hundreds of relevant websites.
    - **Source Links:** Include source links for transparency and credibility.
    - **Syndication:** Optionally syndicate content to platforms like Twitter, LinkedIn, and Facebook.
5. **Run the Script:**

    - Click **"Run"** to generate the script.
    - The output will be a 2,300-word script suitable for a 10-minute video.

### Example Output

```markdown
# Exploring Greek Gods' Romantic Tales  Zeus, the king of the Greek gods, was known for his numerous romantic escapades. One of his most famous stories involves Europa, the beautiful daughter of a king. [Source](https://example.com/source)
```
---

## Step 2: Creating Voiceover with 11Labs

### Overview

**11Labs** offers realistic AI-generated voiceovers, allowing you to convert your script into professional-sounding audio without the need for a microphone.

### How-To Instructions

1. **Access 11Labs:**

    - Visit [11Labs](https://www.11labs.com).
    - Navigate to the **Voice Library**.
2. **Select a Voice:**

    - Choose **English (American)** accent.
    - Select a **Male** voice for a more authoritative tone.
3. **Generate Voiceover:**

    - Copy your entire script from SEO Writing AI.
    - Paste it into 11Labs' text-to-speech interface.
    - Preview different voices to find the most suitable one.
    - Once satisfied, download the audio file.

### Example Voices

- **John Doe:** "I've seen things you people wouldn't believe."
- **Detective Carlson:** "I've received an anonymous tip..."

---

## Step 3: Generating AI Images Using Replicate API

### Overview

To create visually appealing videos, you need a series of images that match your script. **Replicate API** allows you to generate AI-powered images automatically.

### How-To Instructions

1. **Set Up Replicate Account:**

    - Go to [Replicate](https://replicate.com) and create an account.
    - Navigate to **Account Settings > Billing** to set up your payment method.
2. **Select Model:**

    - Choose the **Flux Snell** model for faster and cheaper image generation ($0.003 per image).
    - For higher quality, consider the **Flux Pro** model ($0.05 per image).
3. **Obtain API Token:**

    - In the model page, click on **API** and copy your **Replicate API Token**.
4. **Set Up the Python Script:**

    - Install [Visual Studio Code](https://code.visualstudio.com/) if you haven't already.
    - Open Visual Studio Code and create a new file named `script_to_image.py`.
    - Paste the following code into the file:

```python
`import replicate import os  
# Initialize Replicate with your API token
replicate.Client(api_token="YOUR_REPLICATE_API_TOKEN")  def generate_images(script_text, style, num_images):     
# Split the script into sections     
sections = script_text.split('. ')     sections = sections[:num_images]          images = []     for section in sections:         prompt = f"{style}: {section}"         output = replicate.run("flux/snell", input={"prompt": prompt})         images.append(output)          
# Save images to a folder     
if not os.path.exists('generated_images'):         os.makedirs('generated_images')          for idx, img in enumerate(images):         with open(f'generated_images/image_{idx+1}.png', 'wb') as f:             f.write(img)          print("Image generation completed.")  if __name__ == "__main__":     script = """Your script text goes here."""     generate_images(script, style="Mythological highly detailed digital art", num_images=90)`
```
5. **Install Required Packages:**
    - Open the terminal in Visual Studio Code.
    - Run the following command to install the Replicate package:

bash

Copy code

```bash
pip install replicate
```
6. **Run the Script:**
    - Replace `"YOUR_REPLICATE_API_TOKEN"` with your actual API token.
    - Replace `"""Your script text goes here."""` with your generated script.
    - Execute the script by running:

```bash
python script_to_image.py
```
7. **Troubleshooting:**
    - If you encounter errors, copy the error message and consult ChatGPT for assistance.
    - Common fixes include ensuring correct API tokens and installing all dependencies.

---

## Step 4: Assembling the Video in DaVinci Resolve

### Overview

**DaVinci Resolve** is a powerful free video editor that allows you to compile your images and voiceover into a cohesive video.

### How-To Instructions

1. **Download DaVinci Resolve:**

    - Visit DaVinci Resolve and download the latest version.
2. **Import Assets:**

    - Open DaVinci Resolve and create a new project.
    - Import the generated images and the voiceover audio file.
3. **Configure Image Duration:**

    - Navigate to **Edit > Preferences > User > Editing**.
    - Set **Standard Still Duration** to **10 seconds**.
    - Apply and save settings.
4. **Arrange Images on Timeline:**

    - Drag all images onto the timeline.
    - Ensure each image displays for 10 seconds.
5. **Add Voiceover:**

    - Drag the voiceover audio onto the audio track in the timeline.
    - Align it with the images.
6. **Add Transitions and Zoom Effects:**

    - Go to the **Transitions** panel.
    - Select **Luma Wipe** and set it as the default transition.
    - Apply the transition between all image pairs by copying and pasting the transition.
    - To add a continuous zoom:
        - Select the first image.
        - In the **Inspector**, set the initial zoom to **100%**.
        - Move to the end of the clip and set the zoom to **130%**.
        - Copy these keyframes and apply to all images.
7. **Example Transition Setup:**

```markdown
- **Transition:** Luma Wipe - **Duration:** 3 seconds - **Zoom:** 100% to 130%
```
---

## Final Touches

### Adding Music

1. **Access Pixabay:**

    - Visit Pixabay Music to find copyright-free music.
2. **Select and Download Music:**

    - Choose a track that complements your video.
    - Download the selected music file.
3. **Import Music into DaVinci Resolve:**

    - Drag the music file onto the timeline.
    - Extend the music to cover the entire video duration.

### Adding Subtitles

1. **Generate Subtitles:**

    - In DaVinci Resolve, go to **Timeline > Subtitles > Create Subtitles from Audio**.
    - Set **Maximum Characters per Line** to **30**.
    - Click **Create**.
2. **Customize Subtitles:**

    - Select the subtitle track.
    - Change text color to white with a black stroke and drop shadow for better visibility.
3. **Apply Subtitles:**

    - Ensure subtitles are synchronized with the voiceover.

---

## Conclusion

By following these steps, you've successfully created a high-quality YouTube video using AI tools. This automated workflow not only saves time but also ensures consistency and scalability for your content creation efforts.

---

## Useful Links

- [SEO Writing AI](https://www.seowritingai.com)
- [11Labs](https://www.11labs.com)
- [Replicate](https://replicate.com)
- [Visual Studio Code](https://code.visualstudio.com/)
- DaVinci Resolve
- Pixabay Music

[[Python]]