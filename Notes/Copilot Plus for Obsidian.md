---
github_link: https://github.com/logancyang/obsidian-copilot/discussions/726
tags:
- obsidian
- agents
- editors
video-url: https://www.youtube.com/watch?v=tZ2jm_UPc6c&list=WL&index=5
---

## **Copilot Plus for Obsidian

The text is a detailed overview of Copilot Plus, an advanced version of the Obsidian Copilot plugin, which is designed to bring AI-powered features into the Obsidian note-taking environment. Below, I provide a breakdown of all the features mentioned, including how-to instructions and the use of various code and commands to operate Copilot Plus.

### Overview of Copilot for Obsidian

**Copilot for Obsidian** is an AI plugin for the Obsidian note-taking application, which integrates the capabilities of ChatGPT directly into Obsidian. It aims to allow users to leverage AI without switching between applications, making Obsidian more appealing even for non-users of the platform.

### Vision of Copilot Plus

- Logan, the creator, wants Copilot to be more than just a plugin; he envisions it as a tool that brings the best AI experiences into Obsidian.
- The plugin aims to combine strengths from various AI tools (like **Cursor** for coding and **NotebookLM** for working with PDFs and YouTube) to enhance productivity in a Personal Knowledge Management (PKM) context.

### Features and How to Use Copilot Plus

#### 1. **License Key Setup and Initial Configuration**

- **Setting Up Copilot Plus**:
  - **Install Copilot Plugin**: Ensure the base Copilot plugin is installed in your Obsidian vault.
  - **Activate Plus Mode**:
    - Navigate to the plugin settings in Obsidian.
    - Enter your **license key** (currently distributed to early supporters).
    - Hit **Save**.
  - After the activation, you can set Copilot Plus as your **default mode**.

#### 2. **Context Input and Managing Notes**

- **Chat Input Interface**: The chat input is similar to Cursor, offering interaction with AI models and contextual note input.
- **Adding Contextual Notes**:
  - Click the **plus button** to add notes or PDFs for context.
  - You can add the **current active note**, other notes, or PDFs in your vault.
  - Notes and PDFs can be added manually or through commands. You can also **type note titles in square brackets**, which will automatically include them in the context as you type.
  - **Removing Notes**: Click on the **cross** icon next to a note or delete the note title in the text, and it will be removed automatically.
- **Summarization Example**:
  - Add two notes and ask Copilot to **summarize them** separately.
  - The response will contain two separate summaries, one for each part.

#### 3. **Vault Search and Time-Based Queries**

- **Vault Search Mechanism**: The vault search is different from adding context manually.
  - Use `@vault` in your query to trigger a **local search** over your entire vault.
  - **Show Sources Button**: Displays high and low relevant sources in the search results.
  - **Time-Based Queries**: Copilot Plus can perform time-sensitive queries such as "What did I do this week?" by analyzing the **modification times** of notes.
  - **Keyboard Shortcuts** and dedicated buttons are available to trigger these functions conveniently.

#### 4. **Web Search Integration**

- **Querying Web Pages**:
  - Simply provide the URL of a website in your query (e.g., “What’s on ObsidianCopilot.com?”).
  - Copilot Plus fetches content from the site and provides a summary.
- **Handling Complex Content**:
  - Copilot Plus can also summarize lengthy PDFs (e.g., a **49-page paper from arXiv**).
  - Ask specific questions (e.g., "Figure 1, distribution of Iris flower") for detailed insights from charts and diagrams.

#### 5. **PDF Reading and Interaction**

- **Adding PDFs to Context**:
  - Download a PDF and add it to the context just like a normal note.
  - Ask questions based on the content, and the AI will provide specific details.
- **Embedded PDFs**:
  - You can also **embed a PDF in a Markdown note**.
  - Ask a question directly about the embedded PDF, such as “Who are the authors?” to receive an answer extracted from the PDF content.

#### 6. **Image Support**

- **Adding Images**:
  - Images can be added to the context using an **image container**.
  - This feature allows for removing images or switching between different models.
- **Image Analysis Example**:
  - Copilot Plus analyzed an image of a **Chinese-English bilingual sign**. The model provided corrections for incorrect translations and understood the humor behind the translation error.

#### 7. **Handling Unsupported Features**

- Some models, like **Haiku**, do not support image input. If this happens, Copilot will provide an error, such as “Haiku does not support image input,” ensuring that users know which models can handle which features.

#### 8. **Web Search with Context**

- **Real-Time Web Search**:
  - Copilot Plus can also do **web searches** for real-time data. For example, it successfully retrieved information regarding a **recent PSE power outage**.
  - After the web search, Copilot Plus lists **sources** at the end of its response for transparency.

#### 9. **YouTube Video Integration**

- **Getting YouTube Transcripts**:
  - Use the **YouTube tool** by entering a video URL.
  - The tool quickly retrieves the transcript (e.g., a **2.5-hour Huberman Lab Podcast**) and can summarize it into bullet points.
  - Currently, only **videos in English** are supported.

### Key Demonstrations and Examples

1. **Summarizing Notes**:
   - Copilot Plus can handle multiple notes at once, giving separate summaries for each.
2. **Vault Search and Time Queries**:
   - Useful for retrieving modified notes or understanding past activities by searching through the note history.
3. **Web Search with URLs**:
   - Direct integration of web search, including papers from arXiv, gives a new dimension for research directly within Obsidian.
4. **PDF Handling**:
   - The ability to process embedded PDFs allows users to seamlessly interact with complex content, such as **NASA reports or academic papers**.
5. **Image Analysis**:
   - With models that support image input, Copilot Plus can interpret humorous translation fails and suggest corrections.
6. **Real-Time Information**:
   - Web search allows Copilot Plus to be used for gathering real-time updates without leaving the Obsidian environment.
7. **YouTube Integration**:
   - Fetching transcripts from YouTube is a great feature for extracting key information from educational videos or podcasts.

### Conclusion and Future Developments

- **Alpha Version**: This is still an **alpha version** of Copilot Plus, and future enhancements will be heavily influenced by community feedback.
- **User Input**: Users are encouraged to provide feedback, as the plugin will evolve to better suit their needs.
- **Invitation**: Interested users are invited to **sign up for the waitlist** at [obsidiancopilot.com](http://obsidiancopilot.com) to get notified when the full version is available.

### Summary

Copilot Plus aims to enhance the use of Obsidian by adding powerful AI-driven capabilities:

- Summarizing notes and analyzing PDFs
- Searching through a user’s entire vault
- Handling contextual data like images and PDFs
- Performing web searches
- Integrating YouTube video transcripts

With these features, Copilot Plus aims to bring together the best of AI tools like ChatGPT, and integrate them seamlessly into your second brain, enabling a rich, contextually aware personal knowledge management experience.

[[Obsidian]]      [[Code Editor]]