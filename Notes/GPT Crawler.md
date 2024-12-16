---
tags:
- python
- gpt
- web-scrapper
video-url: https://www.youtube.com/watch?v=jNKDxUkON68&list=WL&index=13
---

## **GPT Crawler**

This transcript discusses a tool called **GPT Crawler**, which allows users to crawl a website and generate knowledge files for creating a custom GPT (Generative Pre-trained Transformer) or other LLM (Large Language Model) applications. The tool can extract documents from one or multiple URLs to help with building AI systems. Here's a detailed summary of the key points, along with relevant how-to instructions and code snippets:

### 1. **Introduction to GPT Crawler**

- GPT Crawler is a simple, lightweight tool designed to crawl websites and create structured knowledge files (in JSON format) that can be used with a custom GPT, AI agents, or other LLM tools like Cursor.
- It's particularly useful for gathering data for AI training, enabling integration with OpenAI's API or other applications to enhance LLMs with specific, custom data.

**Use Cases:**

- Custom GPT models
- AI assistants trained on specific documents
- Scraping websites for structured knowledge
- API integration with OpenAI

### 2. **How to Set Up GPT Crawler**

#### **Step 1: Clone the GitHub Repository**

The first step is to clone the GPT Crawler repository using the following command:

```bash
git clone [REPO_URL]
```

After cloning, navigate to the directory:

```bash
cd GPT-crawler
```

#### **Step 2: Open the Project in a Code Editor**

To work on the project easily, you can open it in Visual Studio Code (VS Code):

```bash
code .
```

#### **Step 3: Modify the Config File**

In the **source** directory, open the `config.sys` file to customize your crawl parameters:

- **URL to crawl**: Define the starting URLs.
- **Selector**: Use specific CSS selectors to extract the content you want, such as text without headers and footers.
- **Max Pages**: Limit the number of pages to crawl (e.g., 50 pages).
- **Output**: Specify the format and file name for the output (e.g., `output.json`).

#### **Example config.sys:**

```bash
{   "urls": ["https://example.com/docs"],   "selector": ".doc-container",   "maxPages": 50,   "outputFile": "output.json" }
```

#### **Step 4: Run the Crawler**

To start the crawling process, use the following command:

```bash
npm start
```

The crawler uses **Playwright**, a headless browser tool, and starts extracting the specified content. It doesn’t require any API keys or tokens, making it cost-effective.

### 3. **How GPT Crawler Works**

- The tool uses Playwright to visit the specified URLs and crawl up to the maximum number of pages.
- The **CSS selectors** in the config file ensure that only the desired content (like article text) is extracted, excluding unwanted parts like headers or footers.
- The data is then stored in JSON format, which can be easily imported into tools like Cursor or fine-tuned in other LLMs.

#### **Output Example:**

After crawling, the `output.json` file contains:

- The page title
- URL
- Extracted HTML content

This content can be further processed or cleaned if necessary.

### 4. **Advanced Options**

- **Docker Support**: For users familiar with Docker, the crawler can also be run using a Docker container.
- **API Integration**: Once the data is collected, you can upload it to OpenAI or other platforms to create a custom-trained GPT model.

### 5. **Use Cases for Other Tools**

The video also references other similar tools like **Fire Crawl** and **Crawl for AI** that offer alternative approaches to crawling websites and collecting data for LLMs. These tools allow for more advanced data cleaning and customization.

### 6. **Conclusion and Resources**

- GPT Crawler is an easy-to-use tool that simplifies the process of gathering data for LLM training.
- The video encourages users to explore other AI tools and the creator’s other tutorials on **AI agents** and the **Stride AI agents repo**.

**Related URLs and Resources**:

- [GPT Crawler GitHub Repository (Not specified in the text, would likely be found on GitHub)].
- [OpenAI API documentation](https://platform.openai.com/docs) for integrating custom models.
- [Playwright Documentation](https://playwright.dev/) for learning more about the tool used for web scraping.
- [Stride Agents](https://strideagents.com) for AI-powered appointment setters.

### Additional Tools Mentioned:

- **Fire Crawl**
- **Crawl for AI**
- **Cursor (IDE for LLMs)**
- **Stride AI agents**

The tutorial in the video emphasizes the importance of gathering high-quality data for AI training and how tools like GPT Crawler help automate the process efficiently, without needing advanced coding skills.

[[GPT]]   [[Web Scrapping]]