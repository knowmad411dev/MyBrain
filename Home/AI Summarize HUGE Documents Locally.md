---
tags:
- ollama
- langchain
- python
- home
video-url: https://www.youtube.com/watch?v=Gn64NNr3bqU&list=WL&index=2
---

## **AI Summarize HUGE Documents Locally

### **Overview**

The tutorial describes how to **summarize a very large document**, like a 500-page or even 1000-page PDF, using **K-means clustering**. The author explains the shortcomings of trying to feed the entire text to a language model and offers an alternative solution that clusters sections of the text and only uses representative samples for summarization. The main components involve extracting text from a PDF, clustering that text using K-means, and then summarizing representative texts with an LLM.

### **Problems with Basic Summarization**

1. **Context Window Limitations**: Large LLMs have context window size limits, meaning they can only process a certain number of tokens (words) at a time. Feeding an entire large document could exceed this limit.
2. **High Cost and Inefficiency**: Sending a large volume of text to third-party LLMs can be expensive and slow. It could also lead to incomplete summaries if the middle parts of the text are ignored due to context overflow.

### **Solution: K-means Clustering-Based Summarization**

The proposed solution involves:

1. **Extracting the Text**: Break the document into smaller chunks.
2. **Clustering the Text**: Grouping chunks of similar content into clusters.
3. **Summarizing Only Key Chunks**: Selecting representative chunks from each cluster (i.e., cluster centers) and summarizing these, which leads to an efficient, yet comprehensive summary of the entire document.

### **Steps to Summarize a Large Document Using K-means Clustering**

#### **Step 1: Project Setup and Dependencies**

1. **Dependencies to Install**:
   - **PyPDFLoader**: Used to extract text from PDF documents.
   - **Hugging Face Embeddings**: Used for converting text into vector representations for clustering.
   - **Clustering Filter** and **Chatama**: Chatama is used for leveraging local language models.

2. **Initialization**: Make sure to install the necessary dependencies and set up a project directory.

#### **Step 2: Extract Text from the PDF**

- **Function for Extracting Text**:
  1. Use the `PyPDFLoader` module from **LangChain** to extract text from the PDF.
  2. Split the extracted text into smaller chunks using `RecursiveCharacterTextSplitter`. The suggested chunk size here is **2,000 characters**.

- **Why Split the Text?**
  - Splitting the text into chunks ensures that each part is manageable and helps maintain semantic coherence. These chunks will later be used to generate embeddings for clustering.

#### **Step 3: Define the Main Summarization Function**

- **Parameters for the Function**:
  - **File**: The PDF document.
  - **LLM Model**: The language model used to generate the summary.
  - **Embedding Model**: Used for creating vector representations of text.
- **Clustering Filter Setup**:
  - Use the **clustering filter** to pass embeddings and set the **number of clusters**.
  - Experiment with the **number of clusters** to find an optimal balance. Start with **five clusters** and adjust as needed.
  - **Closest Documents**: Adjust the number of documents returned from each cluster (e.g., return two closest documents from each of five clusters).

#### **Step 4: Generate Clusters Using K-means Clustering**

- Call the earlier defined **extract function** to obtain text chunks from the PDF.
- Use the **embedding model** to transform these chunks into vectors and then pass them to the **K-means clustering** filter.
- **Select Representative Documents**: The clustering filter will output a reduced set of documents by choosing representative documents (cluster centers).

#### **Step 5: Summarize Selected Documents**

- Load a **Summarization Chain** (a sequence of operations) and choose the most basic chain type, called `stuff`, to produce the summary.
- Run the chain on the selected representative documents to generate the summary.

#### **Step 6: Set Up the LLM and Embedding Model**

- **LLM Model Setup**:
  - The LLM model is the one that performs the actual summarization.
  - The tutorial uses **Llama 3.1** for local summarization, which is loaded using **AMA serve**.
  - If using Llama, start by downloading the model (`AMA pull`) and then serve it (`AMA serve`). Set the **temperature to 0** for deterministic, non-creative responses.
  - If you prefer a different model, you can import another module from LangChain.
- **Embedding Model Setup**:
  - Embeddings convert text into vector representations that can be used for clustering.
  - Use an older embedding model like **BGE 1.5** or a newer model like **BGE M3** (depending on available hardware).
  - If using a GPU, set the **device to CUDA** to accelerate computation; otherwise, use **CPU**. If using an Apple device, set the backend to **MPS**.
  - Set **normalize embeddings** to True to enable cosine similarity during clustering.

#### **Step 7: Run the Main Function and Generate Summary**

- Call the **main function**, passing in the parameters (PDF file, LLM model, embedding model).
- **Print the Summary**: Display the generated summary to verify that it meets the expected quality.

### **Tips for Improvement**

1. **Experiment with Clustering Parameters**:
   - Adjust the **number of clusters** and **documents per cluster** to refine the summarization quality.
   - More clusters may yield a more detailed summary, while fewer clusters may generalize better.

2. **Use Custom Summarization Instructions**:
   - Instead of relying solely on a predefined summarization chain, provide custom instructions that allow for targeted summarization (e.g., focusing on specific data points).

### **Example Python Code Walkthrough**

Here’s a concise overview of what the Python code might look like for this process:

1. **Extract Function**:
   - Define a function that takes a PDF and returns text chunks using `PyPDFLoader` and `RecursiveCharacterTextSplitter`.

   ```python
   def extract_text(pdf_path):
       loader = PyPDFLoader(pdf_path)
       extracted_text = loader.load()
       text_splitter = RecursiveCharacterTextSplitter(chunk_size=2000)
       return text_splitter.split_text(extracted_text)
   ```

2. **Main Summarization Function**:
   - Define a function to cluster and summarize.

   ```python
   def summarize_large_document(pdf_path, llm, embedding_model, num_clusters=5, docs_per_cluster=2):
       # Extract text
       texts = extract_text(pdf_path)
       # Create embedding filter
       cluster_filter = ClusteringFilter(embedding_model, num_clusters)
       # Cluster text chunks
       results = cluster_filter.transform_documents(texts)
       # Summarize using LLM
       summarization_chain = load_summarization_chain(llm)
       summary = summarization_chain.run(results)
       return summary
   ```

3. **Model Setup**:
   - **Embedding Model** and **LLM Model Setup** for both CUDA and CPU support.
   - Use `AMA serve` to load the Llama model or select an alternative.

   ```python
   embedding = HuggingFaceEmbeddingModel(model_name='bge-1.5', device='cuda', normalize=True)
   llama_model = load_local_llm('llama-3.1', temperature=0)
   summary = summarize_large_document('document.pdf', llama_model, embedding)
   print(summary)
   ```

### **Summary of the Process**

1. Extract text from the PDF using **PyPDFLoader**.
2. Split text into smaller chunks to improve semantic clustering.
3. Convert chunks to embeddings and perform **K-means clustering**.
4. Select cluster center documents and generate a summary using the **LLM**.
5. Use customizable parameters for clustering and summarization to refine the output.

### **Benefits of This Approach**

- **Scalability**: You can easily summarize documents of 500 pages or more.
- **Efficiency**: By using clustering, you only summarize representative chunks, making the process much faster.
- **Cost-Effective**: Requires less memory, computational resources, and minimizes expensive API calls.

### **Conclusion**

The K-means clustering approach allows you to summarize massive documents more efficiently by focusing on representative parts of the document rather than summarizing everything. This is particularly useful if you are using limited-resource LLMs and want to avoid hitting context window limits or incurring high costs. By experimenting with different clustering parameters and embedding models, you can find the balance that works best for your summarization needs.

[[Ollama]]  [[LangChain]]  [[Python]]  [[LLM]]  [[Home]]