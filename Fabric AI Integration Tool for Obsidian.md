# Fabric: The Best AI Integration Tool For Obsidian
https://www.youtube.com/watch?v=TIXNqBzx3O0

![](https://www.youtube.com/watch?v=TIXNqBzx3O0)
## Summary:

**Summary: Integration of Fabric AI with Obsidian**

This video explains how to integrate Fabric AI, a command-line AI tool, with Obsidian to enhance your note-taking experience without relying on the command-line interface. The integration allows users to summarize videos, articles, podcasts, and more directly within Obsidian.

### Key Points:

- **Introduction to Fabric AI**:
    
    - Fabric AI is a command-line tool that can summarize content from podcasts, articles, and videos, create essays from drafts, and more.
    - This video focuses on integrating Fabric AI with Obsidian for a smoother, GUI-based experience.
- **Installation of Fabric AI**:
    
    - Verify Fabric is correctly installed by running the command `fabric --help` in the terminal. If not installed correctly, refer to the previous video linked in the description.
- **Installing the Unofficial Fabric Integration Plugin**:
    
    - Install the "Unofficial Fabric Integration" plugin via Obsidian’s community plugins section.
    - Reload Obsidian to access the integration features.
- **Fabric Integration Setup**:
    
    - Add the Fabric API URL and API key in the plugin settings.
    - If errors occur, enable the compatibility mode for Fabric 2.0 (the latest version).
- **Configuring Settings**:
    
    - Set the output folder for saving processed notes.
    - Configure a custom patterns folder for advanced use cases.
    - By default, the Lama 3.1 model is used, but other models can be selected if available.
- **YouTube Video Processing Example**:
    
    - Copy a YouTube video link, set the file name, and select patterns such as "Extract Wisdom" to summarize the content.
    - Pattern chaining is available: multiple patterns can be applied sequentially (e.g., "Extract Wisdom" followed by "Rate Value").
- **Other Use Cases**:
    
    - Process existing notes using patterns like "Improve Writing" or "Write an Essay."
    - Audio processing is possible but only works on macOS (the presenter didn’t explore this feature in detail).
- **TAV (AI-Powered Search Engine)**:
    
    - TAV is a search engine designed for language models (LLMs).
    - The video demonstrates how to connect Fabric to TAV and use patterns to process search results directly into a markdown note in Obsidian.
- **Creating Custom Patterns**:
    
    - Users can create custom patterns, such as "Write an Essay in My Voice."
    - Once a custom pattern is uploaded, it will appear in the Fabric tool for use in note generation.
- **Future Development**:
    
    - The creator of the "Unofficial Fabric Integration" is developing a new plugin, MES AI, which will eliminate the need for the Fabric command line and connector tools.

### Final Thoughts:

The integration of Fabric AI with Obsidian offers a powerful way to automate note creation and content summarization. While future improvements may streamline the setup, this guide provides a step-by-step approach to using Fabric AI efficiently within Obsidian.

Here is a list of the step-by-step instructions provided in the video:

### 1. **Installing Fabric AI**:

- Open the terminal and run the command: `fabric --help` to verify installation.
- If Fabric AI isn’t installed, refer to the previous video for installation guidance.

### 2. **Installing the Unofficial Fabric Integration Plugin**:

- Open Obsidian.
- Go to **Settings** > **Community Plugins**.
- Search for "Unofficial Fabric Integration" by "changee Bank."
- Click **Install**, then **Enable**.
- Reload Obsidian to apply changes.

### 3. **Setting Up the Unofficial Fabric Integration Plugin**:

- Open **Settings** > **Unofficial Fabric Integration**.
- In the plugin options, add the **Fabric API URL** and **API Key**:
    1. Go to the GitHub repository of the plugin and find the link to download the **Fabric Connector**.
    2. Download the appropriate version for your operating system (Mac or Windows).
    3. Install the Fabric Connector and launch the app.
    4. From Obsidian, click on the brain icon in the menu bar.
    5. Copy the Fabric API URL (after `http://` and before `/docs`) and the API key.
    6. Paste both into the plugin’s settings in Obsidian.
- Enable **Compatibility Mode** for Fabric 2.0 (if necessary) to avoid errors.
- Click **Test API** to ensure the integration works.

### 4. **Configuring Output and Patterns Folder**:

- In the plugin settings, set the **Output Folder** where the tool will save files (e.g., “Fabric Tools”).
- Set the **Patterns Folder** where custom patterns can be stored for use with the tool.

### 5. **Summarizing YouTube Videos**:

- Copy a YouTube link.
- Go to the Fabric tool in Obsidian, give the output file a name (e.g., "YouTube Summary").
- Enable **YouTube Link Detection**.
- Choose a **Pattern** like "Extract Wisdom" or chain multiple patterns.
- Click **Run** to process the YouTube video.

### 6. **Using Fabric to Process Notes**:

- Open an existing note in Obsidian.
- Select a pattern such as **Improve Writing** or **Write an Essay**.
- Run the tool to improve the note’s content based on the selected pattern.

### 7. **Setting Up TAV Search Integration**:

- Go to the TAV website and sign up for an account.
- Create an API key from the TAV dashboard.
- In Obsidian, go to **Unofficial Fabric Integration** settings and paste the TAV API key.
- Download the **Search Engine Pattern** for TAV from the plugin's GitHub repository and save it in the Patterns Folder.
- Refresh the patterns in the plugin, and the TAV pattern will now be available for use.

### 8. **Creating and Using Custom Patterns**:

- In the **Patterns Folder**, create a new note for a custom pattern (e.g., "Write an Essay in My Voice").
- Add the prompt for the custom pattern inside the note.
- Upload the custom pattern via the Fabric plugin in Obsidian.
- Use the custom pattern by selecting it from the available patterns list.

By following these steps, you can fully integrate and utilize Fabric AI within Obsidian.

Here is a list of the resources mentioned in the video along with associated links (where applicable):

### 1. **Fabric AI**:

- Command-line AI tool for summarizing content, creating essays, etc.
- [Fabric AI Documentation (GitHub)](https://github.com/fabricai)

### 2. **Unofficial Fabric Integration Plugin**:

- Obsidian plugin to integrate Fabric AI with a GUI.
- **Community Plugin in Obsidian**: Search "Unofficial Fabric Integration" by "changee Bank" in Obsidian’s community plugins section.

### 3. **Fabric Connector**:

- Tool needed to connect Fabric AI with Obsidian.
- [Fabric Connector GitHub Repository](https://github.com/changeebank/fabric-connector)

### 4. **TAV (Search Engine for LLMs)**:

- AI-powered search engine used to process web results and generate markdown notes.
- [TAV Official Website](https://www.tav.com)
- **Create an Account & API Key**: After signing up, create an API key in the TAV dashboard for integration with Fabric AI.

### 5. **Search Engine Pattern for TAV**:

- A specific pattern designed to process search results using TAV.
- Available on the GitHub repository of the Unofficial Fabric Integration plugin.

### 6. **Llama 3.1 Model**:

- The default language model used for text generation within Fabric AI.
- No specific download link; it is included as part of the Fabric AI tool.

These resources help you set up and use Fabric AI within Obsidian for processing various types of content.

