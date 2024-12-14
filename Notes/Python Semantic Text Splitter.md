---
Video-URL: https://www.youtube.com/watch?v=W_yGjKLcViA&list=WL&index=2
tags:
- python
- llm
---

## **Python Semantic Text Splitter

### Detailed Summary: Optimal Document Chunking for Creating Embeddings Using Semantic Text Splitter

When creating embeddings for documents, determining the ideal chunk size is crucial for ensuring meaningful and effective representations. Traditional methods often use fixed chunk sizes (e.g., 50, 100, 500 characters), but this approach can lead to fragmented or mixed-topic chunks, resulting in poor performance in downstream applications such as information retrieval or question-answering systems.

**This summary explores an alternative approach called **[**Semantic Text Chunking**](#semantic-text-chunking)** using the **[**Semantic Text Splitter**](#semantic-text-splitter)** package, which leverages model-based techniques to create more coherent and topic-specific chunks.**

---

### Table of Contents

1. [Traditional vs. Semantic Chunking](#traditional-vs-semantic-chunking)
2. [Introducing Semantic Text Splitter](#introducing-semantic-text-splitter)
3. [Step-by-Step Guide](#step-by-step-guide)
    - [1. Installation](#1-installation)
    - [2. Preparing the Text Data](#2-preparing-the-text-data)
    - [3. Traditional Chunking with LangChain](#3-traditional-chunking-with-langchain)
    - [4. Semantic Chunking with Semantic Text Splitter](#4-semantic-chunking-with-semantic-text-splitter)
4. [Comparing Embeddings](#comparing-embeddings)
5. [Visualization and Evaluation](#visualization-and-evaluation)
6. [Conclusion and Recommendations](#conclusion-and-recommendations)
7. [Resources and Links](#resources-and-links)

---

### Traditional vs. Semantic Chunking

**Traditional Chunking** involves splitting text into fixed-size segments based on character or word count. While straightforward, this method doesn't account for the semantic coherence of the text, leading to chunks that may split sentences or mix unrelated topics.

**Semantic Chunking**, on the other hand, uses models to identify coherent segments within the text, ensuring that each chunk represents a complete idea or topic. This method enhances the quality of embeddings by maintaining contextual integrity.

---

### Introducing Semantic Text Splitter

**[Semantic Text Splitter](https://github.com/your-repo/semantic-text-splitter)** is a package designed to perform semantic text chunking. It leverages transformer models to understand the context and structure of the text, enabling the creation of meaningful and topic-specific chunks.

---

### Step-by-Step Guide

#### 1. Installation

First, install the necessary packages:

```
`pip install langchain semantic-text-splitter`
```
> **Note:** Ensure you have Python installed. Semantic Text Splitter is written in Rust for performance, but it integrates seamlessly with Python.

#### 2. Preparing the Text Data

Assume you have a text file named `bank.txt` containing information about a bank and a restaurant:

```text
`Bank of An Example Bank... [Bank-related text] Restaurant XYZ... [Restaurant-related text]`
```

This file includes two distinct topics: banking and restaurant services.

#### 3. Traditional Chunking with [[LangChain]]

**LangChain** provides tools for text loading and splitting. Here's how to perform traditional chunking:

```python
from langchain.text_splitter 
import RecursiveCharacterTextSplitter 
from langchain.document_loaders 
import TextLoader  
# Load the text file 
loader = TextLoader("bank.txt") documents = loader.load()  
# Initialize the text splitter 
text_splitter = RecursiveCharacterTextSplitter(chunk_size=200, chunk_overlap=0 )
# Split the text into chunks chunks = text_splitter.split_documents(documents)  
# Display the number of chunks 
print(f"Number of chunks (LangChain): {len(chunks)}")  
# Example output of a chunk 
print(chunks[0].page_content)
```

**Issues with Traditional Chunking:**

- Chunks may contain incomplete sentences or mixed topics.
- Example: A chunk might only have the bank's name without additional context or mix bank and restaurant information.

#### 4. Semantic Chunking with Semantic Text Splitter

To achieve more meaningful chunks, use the Semantic Text Splitter:

```python
from semantic_text_splitter import SemanticTextSplitter 
# Load the text content using Python's built-in open function 
with open("bank.txt", "r", encoding="utf-8") as file: content = file.read()  
# Initialize the Semantic Text Splitter 
splitter = SemanticTextSplitter( model_name="bert-base-uncased",  
# Hugging Face model
	max_tokens=200, min_tokens=100  
# Optional: 
	set minimum tokens per chunk )  
# Create semantic chunks 
semantic_chunks = splitter.split_text(content)  
# Display the number of semantic chunks 
print(f"Number of chunks (Semantic Text Splitter): {len(semantic_chunks)}")  
# Example output of a semantic chunk 
print(semantic_chunks[0])
```

**Advantages of Semantic Chunking:**

- Chunks align with complete sentences or topics.
- Reduces the risk of mixing unrelated information.
- Enhances the quality of embeddings by maintaining context.

---

### Comparing [[Embeddings]]

After chunking the text, the next step is to create embeddings for each chunk and compare their effectiveness.

```python
from langchain.embeddings import OpenAIEmbeddings import os  
# Set your OpenAI API key 
os.environ["OPENAI_API_KEY"] = "your-api-key"  
# Initialize the embeddings 
embeddings = OpenAIEmbeddings()  
# Create embeddings for traditional chunks 
traditional_embeddings = embeddings.embed_documents([chunk.page_content 
	for chunk in chunks])  
# Create embeddings for semantic chunks 
semantic_embeddings = embeddings.embed_documents(semantic_chunks)
```

#### Example Query and Cosine Similarity

```python
from sklearn.metrics.pairwise 
    import cosine_similarity 
    import numpy as np  
# Define a query 
query = "What does your bank do for the local community?"  
# Embed the query 
query_embedding = embeddings.embed_query(query)  
# Calculate cosine similarity with traditional 
embeddings cos_sim_traditional = cosine_similarity([query_embedding],    traditional_embeddings)[0]  
# Calculate cosine similarity with semantic embeddings 
cos_sim_semantic = cosine_similarity([query_embedding], semantic_embeddings)[0]  
# Retrieve top matches 
top_traditional = np.argsort(cos_sim_traditional)[::-1] 
top_semantic = np.argsort(cos_sim_semantic)[::-1]  
print("Top matches (Traditional Chunking):") 
for idx in top_traditional[:3]:     
    print(f"Score: {cos_sim_traditional[idx]:.4f}, 
    Chunk: {chunks[idx].page_content[:100]}")  
    print("\nTop matches (Semantic Chunking):") for idx in top_semantic[:3]: 
    print(f"Score: {cos_sim_semantic[idx]:.4f}, 
    Chunk: {semantic_chunks[idx][:100]}")
```

**Findings:**

- **Traditional Chunking** may return multiple chunks with mixed topics, leading to irrelevant or incomplete answers.
- **Semantic Chunking** retrieves more relevant and coherent chunks, enhancing the quality of the response.

---

### Visualization and Evaluation

Visualizing embeddings can provide insights into the clustering and separation of topics.

```python
import matplotlib.pyplot as plt from sklearn.decomposition 
import PCA  
# Combine all embeddings 
all_embeddings = traditional_embeddings + semantic_embeddings  
# Reduce dimensions for visualization 
pca = PCA(n_components=2) reduced_embeddings = pca.fit_transform(all_embeddings)  # Plot traditional chunks 
plt.scatter(reduced_embeddings[:len(traditional_embeddings), 0],     reduced_embeddings[:len(traditional_embeddings), 1], label='Traditional',     alpha=0.6 )  
# Plot semantic chunks 
plt.scatter(reduced_embeddings[len(traditional_embeddings):, 0],     reduced_embeddings[len(traditional_embeddings):, 1],     
	label='Semantic', alpha=0.6 )  
	plt.legend() 
	plt.title("Embedding Visualization: Traditional vs. Semantic Chunking") plt.show()
```

**Insights:**

- **Semantic Chunks** tend to cluster more coherently based on topics.
- **Traditional Chunks** may scatter across different topics, indicating mixed or fragmented information.

---

### Conclusion and Recommendations

- **Avoid Fixed-Size Chunking:** Fixed chunk sizes can disrupt the semantic integrity of the text, leading to poor embedding performance.
- **Adopt Semantic Chunking:** Utilizing models to create semantically coherent chunks ensures that each chunk encapsulates complete ideas or topics, enhancing the quality of embeddings.
- **Use Semantic Text Splitter:** The [Semantic Text Splitter](https://github.com/your-repo/semantic-text-splitter) package offers an effective and performant solution for semantic chunking, leveraging transformer models like BERT.
- **Visualize and Evaluate:** Always visualize and evaluate the embeddings to ensure that the chunking strategy aligns with your application's requirements.

---

### Resources and Links

- **Semantic Text Splitter:**
    - GitHub Repository: [https://github.com/your-repo/semantic-text-splitter](https://github.com/your-repo/semantic-text-splitter)
    - PyPI: [https://pypi.org/project/semantic-text-splitter/](https://pypi.org/project/semantic-text-splitter/)
- **LangChain:**
    - Official Website: [https://langchain.com/](https://langchain.com/)
    - Documentation: https://docs.langchain.com/
- **Hugging Face Models:**
    - Model Repository: https://huggingface.co/models
    - BERT Models: https://huggingface.co/bert-base-uncased
- **OpenAI Embeddings:**
    - Documentation: [https://platform.openai.com/docs/guides/embeddings](https://platform.openai.com/docs/guides/embeddings)
- **Python Packages:**
    - Install via PyPI: `pip install langchain semantic-text-splitter`
- **Visualization Libraries:**
    - Matplotlib: [https://matplotlib.org/](https://matplotlib.org/)
    - Scikit-learn PCA: https://scikit-learn.org/stable/modules/generated/sklearn.decomposition.PCA.html

---

By adopting semantic chunking strategies and leveraging tools like Semantic Text Splitter, you can significantly enhance the quality and effectiveness of your document embeddings, leading to better performance in various natural language processing applications.

[[LLM]]   [[Python]]
