---
Video-URL: https://www.youtube.com/watch?v=GMlSFIp1na0&list=WL&index=3
tags:
- ollama
---

**Summary of the Video**

In this video, Matt Williams, a founding member of the Ollama team, explains how to integrate web search functionality into local AI models using Ollama and SearXNG. This integration allows AI models to access the latest information from the internet, overcoming the limitation of models being restricted to their training data or manually added information via Retrieval-Augmented Generation ([[RAG]]).

---

**Understanding the Problem**

- **AI Models' Limitations**: AI language models, such as those used in Ollama, are generally confined to the data they were trained on. They cannot access real-time information or perform web searches independently.
- **Need for Web Search Integration**: To provide up-to-date responses, AI models require access to current information from the web.

**Solution Overview**

- **Web Search Integration**: Incorporating a web search API into the AI workflow allows models to fetch and utilize the latest information from the internet.
- **SearXNG**: Matt introduces [SearXNG](https://github.com/searxng/searxng), a privacy-focused meta-search engine that aggregates results from multiple search engines without tracking user data.

**Why SearXNG?**

- **Privacy Concerns**: Using popular search engines like Google or Bing directly may compromise user privacy, as these services often track and store search data.
- **Meta Search Engine**: SearXNG acts as an intermediary, stripping personal information from queries before sending them to search engines.
- **Self-Hosting**: Users can self-host SearXNG, ensuring full control over their data and search queries.

---

**Step-by-Step Guide**

### 1. Setting Up SearXNG

**Option A: Use a Public Instance**

- Use one of the many public SearXNG instances. However, this means trusting the provider with your data.

**Option B: Self-Host SearXNG Using Docker**

**Prerequisites**: Install [[Docker]].

**Instructions**:

- **Pull the SearXNG Docker Image**:

    ```
    docker pull searxng/searxng
    ```

- **Run the Docker Container**:

    ```
    docker run -d -p 8888:8080 searxng/searxng
    ```

    This command runs SearXNG in a Docker container, mapping port `8080` inside the container to port `8888` on your local machine.

- **Verify the Installation**: Open your browser and navigate to `http://localhost:8888`. You should see the SearXNG search page.

**Alternative: Use Docker Compose**

For a production-ready setup or additional customization, you can use Docker Compose with a `docker-compose.yml` file.

**Resources**: [SearXNG Docker Documentation](https://github.com/searxng/searxng-docker)

---

### 2. Integrating SearXNG with Ollama

**Prerequisites**:

- **Ollama**: Install Ollama by following instructions on [ollama.ai](https://ollama.ai/).
- **Deno**: Install Deno from [deno.land](https://deno.land/).

**Integration Process**:

1. **User Query Input**: Capture the user's question or query.
2. **Search Using SearXNG**: Send the query to SearXNG to get relevant URLs.
3. **Fetch and Clean Web Pages**: Download the content from the URLs and extract the text.
4. **Generate AI Response**: Feed the original query and the extracted text into Ollama to produce an informed answer.

---

### 3. Code Implementation

**Language and Tools**:

- **TypeScript**: Using Deno for execution.
- **Cheerio**: For HTML parsing and text extraction.
- **Ollama**: To run the AI model.

**Code Breakdown**:

#### Imports and Constants

```typescript
import { cheerio } from "https://deno.land/x/cheerio@1.0.7/mod.ts";

const SEARXNG_URL = "http://localhost:8888/search";
const MAX_RESULTS = 5;
```

#### Main Function

```typescript
async function main() {
  const query = "Tell me about the dock workers' strike.";
  console.log(`Query: ${query}`);

  const urls = await getNewsUrls(query);
  const texts = await getCleanedText(urls);
  await answerQuery(query, texts);
}

main();
```

#### Function to Get News URLs

```typescript
async function getNewsUrls(query: string): Promise<string[]> {
  const params = new URLSearchParams({
    q: query,
    format: "json",
    categories: "general",
  });

  const response = await fetch(`${SEARXNG_URL}?${params}`);
  const data = await response.json();

  const urls = data.results.map((result: any) => result.url);
  return urls.slice(0, MAX_RESULTS);
}
```

#### Function to Fetch and Clean Text

```typescript
async function getCleanedText(urls: string[]): Promise<string[]> {
  const texts: string[] = [];

  for (const url of urls) {
    try {
      const response = await fetch(url);
      const html = await response.text();
      const text = htmlToText(html);
      texts.push(text);
    } catch (error) {
      console.error(`Error fetching URL ${url}:`, error);
    }
  }

  return texts;
}
```

#### Function to Convert HTML to Text

```typescript
function htmlToText(html: string): string {
  const $ = cheerio.load(html);

  // Remove unwanted elements
  $("script, style, img, iframe, nav, footer, header").remove();

  // Extract text
  const text = $("body").text();

  // Clean up whitespace
  return text.replace(/\s+/g, " ").trim();
}
```

#### Function to Generate AI Response

```typescript
async function answerQuery(query: string, texts: string[]) {
  const context = texts.join("\n\n");
  const prompt = `${context}\n\nBased on the above information, answer the following question:\n\n${query}`;

  const process = Deno.run({
    cmd: ["ollama", "run", "llama2", "--prompt", prompt],
    stdout: "piped",
    stderr: "piped",
  });

  const output = await process.output();
  const decoder = new TextDecoder();
  console.log(decoder.decode(output));

  process.close();
}
```

**Note**: Replace `"llama2"` with the name of the model you have installed in Ollama.

---

### 4. Running the Code

**Save the Code**: Save the code in a file named `app.ts`.

**Execute the Code**:

```
deno run --allow-net --allow-run app.ts
```

- `--allow-net`: Grants network access for fetching URLs.
- `--allow-run`: Allows the script to run subprocesses (needed for calling Ollama).

**Expected Output**: The AI model will generate a response to the user's query based on the latest information fetched from the web.

---

### 5. Enhancements and Tips

- **Parallel Fetching**: Improve performance by fetching URLs concurrently using `Promise.all()`.
- **Error Handling**: Add comprehensive error handling for network requests and parsing.
- **Text Preprocessing**: Enhance the `htmlToText` function to remove more unwanted content or prioritize certain sections.
- **Customization**: Modify the prompt provided to Ollama to better suit the context.
- **Privacy Settings**: Ensure that your SearXNG instance is configured with the desired privacy settings.

---

**Related Links**

- **Ollama Official Website**: [ollama.ai](https://ollama.ai/)
- **SearXNG GitHub Repository**: [github.com/searxng/searxng](https://github.com/searxng/searxng)
- **Deno Official Website**: [deno.land](https://deno.land/)
- **Cheerio Library**: [deno.land/x/cheerio](https://deno.land/x/cheerio)

---

**Conclusion**

By integrating SearXNG with Ollama, you can enhance your AI applications to provide up-to-date responses using the latest information from the web while maintaining user privacy. This approach leverages self-hosted tools and open-source software to create a powerful and private AI assistant.

---

**Additional Resources**

- **Matt Williams' GitHub Repository**: You can find the source code and more examples in Matt's GitHub repository: [github.com/mattwilliams06/videoprojects](https://github.com/mattwilliams06/videoprojects) (Navigate to the folder with the date `2023-10-01` and then to `websearch`).

**Frequently Asked Questions**

1. **Why use Deno instead of Node.js?**

    - Deno is a modern runtime for JavaScript and TypeScript that comes with built-in support for TypeScript, security by default, and a simpler module system.

2. **Can I use a different AI model with Ollama?**

    - Yes, Ollama supports multiple AI models. You can replace `"llama2"` with the name of the model you have installed.

3. **Is it necessary to self-host SearXNG?**

    - While not mandatory, self-hosting SearXNG ensures maximum privacy and control over your search queries.

4. **How do I customize the search engines used by SearXNG?**

    - You can modify the `settings.yml` file in your SearXNG installation to include or exclude specific search engines.

---

[[Ollama]]