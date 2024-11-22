---
Video-URL: https://www.youtube.com/watchv=TIXNqBzx3O0&list=PLSB1K9AiS9FaHHoiZBfN_K3fo9i8gdNoS&index=7
tags: [Fabric, Obsidian, youtube]
---

## **Fabric Obsidian Integration**

### Step 1: Ensure Fabric AI is Installed

1. **Open a terminal**.
2. Run the command:

```bash
    fabric --help
```
    This should display available options for Fabric AI.

    - If not, refer to the previous installation video linked in the video description.

### Step 2: Install the "Unofficial Fabric Integration" Plugin in Obsidian

1. Open **Obsidian**.
2. Go to **Settings** > **Community Plugins**.
3. Click **Browse**, search for **"Unofficial Fabric Integration"**, and install the plugin by **Changi Bank**.
4. After installation, click **Enable**.
5. Restart Obsidian to activate the plugin.

### Step 3: Set Up the Plugin

1. Go to **Settings** > **Unofficial Fabric Integration**.
2. **Install the Fabric Connector**:
    - Go to the [[GitHub]] repository of the plugin and follow the instructions to install the connector for your operating system (e.g., Windows or macOS).
    - Download and install the connector.
3. Start the **Fabric Connector** app.

### Step 4: Configure API Settings in Obsidian

1. In Obsidian’s **Unofficial Fabric Integration** settings:
    - Click **Open API Docs** and copy the API URL.
    - Paste the copied URL into the **Fabric API URL** field.
2. Click **Copy API Key** in the Fabric Connector and paste it into the **API Key** field in Obsidian.
3. Test the API connection by clicking **Test API**.
    - If there is an error, enable **Compatibility Mode** for Fabric 2.0.

### Step 5: Set Output Folders

1. In the **Unofficial Fabric Integration** settings:
    - Set the **Output Folder** where files created by Fabric will be saved (e.g., "Fabric").
    - Set the **Patterns Folder** for storing custom patterns.

### Step 6: Example Use Case - Summarize a YouTube Video

1. Copy a YouTube video link.
2. In Obsidian, write a file name (e.g., **YouTube Summary**).
3. Enable the option to **Detect YouTube Link**.
4. Choose a **Pattern** (e.g., **Extract Wisdom**).
5. Click **Run** to process the YouTube link and generate a summarized note based on the selected pattern.

### Step 7: Chain Multiple Patterns

1. **Select multiple patterns** for complex tasks:
    - Example: Start with **Extract Wisdom**, followed by **Rate Value**.
    - The first pattern’s output will be fed into the next pattern, with only the final output displayed.

### Step 8: Search the Web Using Tav

1. **Set up Tav**:
    - Create an account on the Tav website and generate an **API key**.
    - Paste the API key into Obsidian's **Unofficial Fabric Integration** settings under **Tav API key**.
2. **Install the Search Engine Pattern** from the plugin’s GitHub page and sync it to Obsidian’s Patterns folder.
3. To search the web, create a new file, enter a query (e.g., "Elon Musk"), and use the **Tav** feature.

### Step 9: Create Custom Patterns

1. In the **Patterns Folder**, create a new note (e.g., **Write an Essay in My Voice**).
2. Write a prompt inside the note that describes what you want the pattern to do.
3. In Obsidian, go to **Unofficial Fabric Integration** and upload this custom pattern.

### Step 10: Improve Prompts Using Fabric

1. Choose the **Improve Prompt** pattern.
2. Use it to enhance any input and fine-tune your writing.

### Summary

By following these steps, you can successfully integrate and use Fabric AI within Obsidian to summarize content, write essays, and more through pre-existing and custom patterns.

---

**Useful Links:**

- [Fabric AI Overview](https://www.fabric.ai/)
- [Obsidian Official Website](https://obsidian.md/)
- [Fabric Connector GitHub Repository](https://github.com/changeebank/fabric-connector)
- [Tav Official Website](https://www.tav.com)

**Tags:** , [[Obsidian]], [[Workflow]], [[Prompting]]

