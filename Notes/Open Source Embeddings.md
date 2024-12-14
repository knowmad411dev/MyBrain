---
Video-URL: https://www.youtube.com/watch?v=QdDoFfkVkcw&list=WL&index=4
tags:
- llm
---

## **Open-Source [[Embeddings]]**

### 1. **Understanding Embeddings**

- **Embeddings** are vector representations of data that capture the semantic meaning of text, images, or other content types.
- OpenAI's **text-embedding-ada-002** is a popular and cost-effective embedding model that costs $0.0001 per 1,000 tokens (as of June 2023).
- **Use Cases for Embeddings**: Beyond simple text search, embeddings can be used for clustering, classification, re-ranking, and retrieval tasks.

#### Examples and Resources

- [Hugging Face](https://huggingface.co/): A central repository for hosting and using machine learning models, including embeddings.
- **Sentence Transformers Library**: A popular Python framework for generating embeddings based on the BERT model and its variants. [SBERT Documentation](https://www.sbert.net/)

### 2. **Comparing Embedding Models**

- There are many open-source embedding models, each with strengths and trade-offs in input size limits, dimension sizes, and computational speed.
- Open-source models offer options for **self-hosting** and running without dependence on third-party APIs.
- **Model Benchmarks and Performance**: Models differ in quality, speed, and their ability to handle various input sequences and tasks.
    - Massive Text Embedding Benchmark (MTEB) by Hugging Face: A leaderboard comparing the performance of various models across multiple embedding tasks.

#### Code & Tools

- **Tokenization**: Convert text into smaller units (tokens) that can be understood by the embedding model. For example, OpenAI's `tiktoken` library and WordPiece Tokenization.
- **Example Tokenizer**: [OpenAI Tokenizer](https://platform.openai.com/tokenizer)

### 3. **Implementing Embeddings with Hugging Face APIs**

- **Hugging Face Inference API**: Provides access to many models that can be used for generating embeddings.
    - **Installation and Usage**: Requires the Hugging Face JS library for TypeScript integration.

        ```
        npm install @huggingface/inference
        ```

    - **Setting up API Access**:

        ```typescript
        import { HfInference } from '@huggingface/inference';
        const hf = new HfInference('YOUR_HUGGING_FACE_API_KEY');
        ```

- **Choosing a Model for Embeddings**:
    - Select a model from the MTEB leaderboard or from the Hugging Face Models.
    - Popular choices include `all-MiniLM-L6-v2` and `E5-small-V2`.
    - **Example Model Usage**:

        ```typescript
        const model = 'sentence-transformers/all-MiniLM-L6-v2';
        const result = await hf.featureExtraction({ model, inputs: 'Your text here' });
        console.log(result); // Outputs embedding
        ```

- **Calculating Embedding Similarity**:
    - Calculate similarity between vectors using the **dot product**, cosine similarity, or Euclidean distance.

    ```typescript
    function dotProduct(a, b) {
      return a.reduce((sum, ai, index) => sum + ai * b[index], 0);
    }
    ```

### 4. **Self-Hosting with Transformers.js**

- **Transformers.js**: A library that allows running machine learning models directly in JavaScript, either in a Node.js environment or in the browser.
    - **Installation**:

        ```
        npm install @xenova/transformers
        ```

    - **Running in Node.js**:

        ```node.js
        import { pipeline } from '@xenova/transformers';
        const generateEmbeddings = await pipeline('feature-extraction', 'sentence-transformers/all-MiniLM-L6-v2');
        const embeddings = await generateEmbeddings('Your text here');
        console.log(embeddings);
        ```

    - **Note**: The library uses **ONNX Runtime** under the hood for efficient inference across different environments, including web and mobile.

#### Deployment & Performance

- **Caching Models**: Transformers.js fetches and caches models locally to speed up subsequent runs.
- **Quantization**: Reduce the precision of model weights (e.g., float32 to int8) to speed up inference and reduce model size. Check the Hugging Face model card for details on quantized versions.

### 5. **Running Embeddings Directly in the Browser**

- **Browser Embedding Generation**: Similar to running in Node.js, you can use Transformers.js directly in the browser using ES module imports.
- **HTML Setup Example**:

    ```node.js
    <script type="module">
      import { pipeline } from 'https://cdn.jsdelivr.net/npm/@xenova/transformers';
      // Your code here
    </script>
    ```

- **Example Application**: Create an input form to accept text, generate embeddings, and calculate similarity on the client-side.

### 6. **Future of Embeddings**

- **Multimodal Embeddings**: Models like **CLIP** from OpenAI enable generating embeddings across different data types (e.g., images and text) within the same vector space.
    - **Applications**: Enables zero-shot classification, image-captioning, and more powerful search across media types.
- **Embed Everything**: The direction is toward efficient multimodal co-embeddings that work across images, text, and potentially other modalities like audio.

#### Key Papers

- [CLIP: Learning Transferable Visual Models From Natural Language Supervision](https://arxiv.org/abs/2103.00020)
- [Embed Everything Paper](https://arxiv.org/abs/2109.04455): Aims to create efficient multimodal embedding methods.

---

This note provides a comprehensive guide on the topic of embeddings, focusing on different open-source options, API-based methods, and the potential to self-host models directly in various environments. Whether you're using embeddings for text, images, or other modalities, the tools and frameworks discussed here offer a variety of options for different use cases and needs.

[[LLM Frameworks]] | [[LLM]]