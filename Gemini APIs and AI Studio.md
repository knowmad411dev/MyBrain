---
tags:
- editors
---
## **Gemini APIs and AI Studio

### Overview of Google AI Studio and Gemini APIs

**Speaker**: Paige Balley, Lead of Developer Experience Team at Google

This session provides an in-depth look at Google AI Studio and Gemini APIs, focusing on how to get started with these tools, their features, and capabilities.

---

### Key Concepts

#### 1. **Generative AI Integration**

- Google integrates AI across all its products:
    
    - **Google Docs, Sheets, and Slides**: AI aids in content generation and editing.
    - **Chrome Browser**: Direct AI integration for improved user experience.
    - **Google Colab**: AI supports code generation, completions, and debugging.
- **DeepMind Contributions**:
    
    - AlphaZero, AlphaFold, and the flagship **Gemini** models.

#### 2. **Gemini Models**

- **Multimodal Capabilities**:
    - Understands **video, images, audio, text**, and **full codebases**.
- **Versions of Gemini**:
    - **Gemini 1.5 Flash**: Production-ready, quick, cost-effective.
    - **Gemini 1.5 Pro**: Up to **2 million token** context window, best for complex tasks.
    - **Gemini Flash 8B**: Tiny, fast, and capable for specific tasks like code execution.
- **Performance**:
    - Consistently ranks highly on LMSYS and Artificial Analysis leaderboards.

#### 3. **2 Million Token Context Window**

- Allows providing vast information to the model **at inference time**.
- Reduces the need for fine-tuning or setting up vector databases.
- Examples of 1-2M tokens:
    - Emails sent over a year.
    - Lifetime of text messages.
    - Hours of video or hundreds of songs.

---

### Getting Started with AI Studio

1. **Accessing AI Studio**:
    
    - URL: [aistudio.google.com](https://aistudio.google.com/).
    - Log in with your **Google account**.
2. **Features of the UI**:
    
    - Upload files from Google Drive or local storage.
    - Record audio or video directly.
    - Use **sample media** provided by Google.
    - Explore a **Prompt Gallery** for inspiration.
3. **Choosing the Right Model**:
    
    - **Gemini 1.5 Pro**: Most capable model.
    - **Flash 8B**: Lightweight, cost-efficient version.
    - **Gemma Models**: Open-source alternatives.
4. **Demo: Video Analysis**:
    
    - Example: Analyze a dinosaur video.
        
    - **Steps**:
        
        - Add video via the UI.
        - Use a prompt:
            
            > "Please tell me the names of all dinosaurs in this video, the timestamp for each, and a fun fact about each."
            
        - Run the model to get results.
    - **Result**: Names, timestamps, and fun facts in seconds.
        
    - **Performance**:
        
        - 5-minute video analyzed in **14 seconds**.
        - Cost efficiency: Analyzing a full day of video costs less than a cup of Starbucks coffee.
5. **Demo: PDF Analysis**:
    
    - Upload a PDF (e.g., _Animorphs_ book).
    - Example Prompt:
        
        > "Please transcribe all the text from page 66."
        
    - Gemini returns accurate transcriptions quickly.
6. **Code Execution with Python**:
    
    - **Feature**: Isolated sandbox for running Python code.
    - Example Prompt:
        
        > "Tell me which day of the week my birthday (September 21) will fall on from 2025 to 2525."
        
    - **Process**:
        - Gemini generates Python code for date calculations.
        - Executes the code and provides results.
    - **Code Example**:
        
        ```python
        import datetime
        def calculate_days(start_year, end_year, month, day):
            days = {}
            for year in range(start_year, end_year + 1):
                date = datetime.date(year, month, day)
                days[year] = date.strftime("%A")
            return days
        results = calculate_days(2025, 2525, 9, 21)
        print(results)
        ```
        
7. **Search Grounding**:
    
    - Integrates **Google Search** results for real-time data.
    - Example Prompt:
        
        > "Who won the Physics Nobel Prize in 2024?"
        
    - Without grounding: Gemini can't answer due to data cut-off.
    - With grounding: Fetches and synthesizes real-time search results.
8. **Exporting Code**:
    
    - AI Studio allows exporting Python or JavaScript code.
    - Automatically generates code based on your actions.
    - Direct Colab integration: One-click export to Colab notebooks.

---

### Function Calling

- Dynamically select tools or external models for task execution.
- Example Use Cases:
    - Querying APIs.
    - Extracting structured data.
    - Running satellite imagery analyzers.

---

### Generating API Keys

- **Steps**:
    1. Navigate to the **"Get API Key"** section in AI Studio.
    2. Click **"Create New API Key"**.
- API keys can be used directly in Colab, Python, or other applications.
- You can also **tune models** with your custom datasets (e.g., CSV files).

---

### Google AI for Startups Program

- Provides **Google Cloud Credits**:
    - Pre-funding Tier: Startup and ecosystem support.
    - Post-funding Tier: Equity-free credits for scaling applications.

---

### Summary

1. **Try AI Studio for Free**: [aistudio.google.com](https://aistudio.google.com/).
2. **Key Capabilities**:
    - Video, PDF, and real-time data analysis.
    - Python code execution and search grounding.
    - Exporting auto-generated code to Colab.
3. **Reach Out**: Contact Paige Balley at _[webpage@google.com](mailto:webpage@google.com)_ for assistance.

---

AI Studio and the Gemini APIs offer powerful tools to enrich applications, enhance productivity, and experiment with cutting-edge generative AI technology. Try it today!

[[Code Editor]]