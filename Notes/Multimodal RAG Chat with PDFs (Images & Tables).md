---
tags:
- rag
- pdf
- gpt
video-url: https://www.youtube.com/watch?v=uLrReyH5cu0&list=WL&index=2
---
## **Multimodal RAG Chat with PDFs (Images & Tables)

Here's a detailed overview and how-to guide for the YouTube transcript you provided, which demonstrates how to build a system for chatting with a PDF document, including processing its images, tables, and other elements. This guide provides both a conceptual understanding and detailed code examples for implementation.

### Overview

The main objective of the tutorial is to develop a pipeline that can extract and interact with all components of a PDF document—text, tables, images, and other media. This includes summarizing and embedding these components in a way that a language model with multimodal capabilities (such as GPT-4) can provide meaningful responses to user queries. Here's a breakdown of the key stages:

1. **Extracting PDF Content with Unstructured**:
   - A library named "Unstructured" is used to parse various elements of a document, breaking them into images, tables, and text.
   - Content is categorized into different arrays to treat them differently for embeddings and further usage.

2. **Summarization of Extracted Content**:
   - Once the elements are extracted, they are summarized using a text-based language model (e.g., GPT-3 or LLaMA).
   - Images are summarized/described using a multimodal language model.

3. **Creating a Multi-Vector Retrieval Pipeline**:
   - All document summaries are embedded and stored in a vector database (using ChromaDB).
   - Full documents are stored in a document database, linked to their summaries by a unique document ID.
   - The multi-vector retriever is used for efficient querying and retrieval based on summaries.

4. **Integration with Multimodal Language Models**:
   - The multimodal input is used to answer questions regarding extracted text, tables, and images, depending on the query.

The transcript walks through the complete setup process for this PDF parsing system, including extraction, summarization, embedding, and retrieval.

### How-To Instructions

Below are step-by-step instructions, along with code examples, to set up and implement the system explained in the transcript:

#### Step 1: Install Necessary Libraries

First, you need to install several dependencies. Depending on your operating system, follow the appropriate setup instructions:

```bash
# Install libraries using pip
pip install unstructured pillow lxml chromadb langchain openai
```

#### Step 2: Extracting Content from PDF Using `Unstructured`

This step involves using the "Unstructured" library to parse the PDF file into individual elements (text, images, tables).

```python
from unstructured.partition.pdf import partition_pdf

# Set up the file path for the PDF document
pdf_file_path = 'path/to/your/pdf_file.pdf'

# Extract the components from the PDF
# Use the high-resolution extraction strategy for better table extraction
extracted_elements = partition_pdf(pdf_file_path, strategy='hi_res', infer_table_structure=True)
```

The output of the above code is an array of elements (text, tables, images). Each of these elements can now be processed individually.

#### Step 3: Chunking PDF Elements

You can further chunk the extracted content using the `chunking` strategy to combine related elements under a common title or topic:

```python
from unstructured.chunking import chunk_by_title

chunks = chunk_by_title(extracted_elements)
```

This combines related elements into coherent chunks, simplifying retrieval and processing later.

#### Step 4: Summarization of Extracted Elements

After extracting and chunking the PDF content, each type of content (text, table, images) is summarized differently.

- **Text Summarization**: Text elements are summarized using language models such as LLaMA or GPT-3.

```python
from langchain import ChatGroq

# Initialize the language model for summarization
language_model = ChatGroq("liap_3.1")

# Summarize each text chunk
summarized_texts = [language_model.summarize(text) for text in chunks['text']]
```

- **Image Summarization**: Images are described using multimodal models like GPT-4 with vision or Gemini.

```python
from openai import OpenAI

# Use a multimodal model to describe images
image_descriptions = [OpenAI().describe_image(image) for image in chunks['images']]
```

- **Table Summarization**: Extract HTML representation and then summarize.

```python
summarized_tables = [language_model.summarize(table.html_representation()) for table in chunks['tables']]
```

#### Step 5: Create Multi-Vector Retrieval Setup

The summaries generated above are stored in a vector database for easy retrieval.

```python
from langchain.vectorstores import ChromaDB
from langchain.retrievers import MultiVectorRetriever
from uuid import uuid4

# Initialize vector database
vector_db = ChromaDB()

# Create document IDs and store summaries
for text_summary in summarized_texts:
    doc_id = str(uuid4())
    vector_db.add_document(doc_id, text_summary)

# Similarly store tables and images summaries...
```

#### Step 6: Building the Retrieval Pipeline

Once everything is stored in the vector database, you build a multi-vector retriever for querying.

```python
# Instantiate multi-vector retriever
retriever = MultiVectorRetriever(
    vector_store=vector_db,
    document_store=full_document_db,
    metadata_id_key='document_id'
)

# Example query
retrieved_docs = retriever.retrieve("What is multi-head attention?")
```

This retriever takes a query and returns relevant documents, including text, images, and tables. The retrieval results are further used for the language model to generate a response.

#### Step 7: Building the Response Pipeline with a Multimodal Model

To generate a response that includes multiple types of context, you need a language model that can process the input, including images.

```python
from langchain.chains import RunnableLambda, RunnablePassThrough

# Define function to parse documents
def parse_documents(retrieved_docs):
    text_parts = [doc['text'] for doc in retrieved_docs if doc['type'] == 'text']
    image_parts = [doc['image'] for doc in retrieved_docs if doc['type'] == 'image']
    return {'text': text_parts, 'images': image_parts}

# Define chain to generate response
response_chain = RunnableLambda(lambda docs: ChatGroq("GPT_40_mini").generate_response(docs))
```

This response pipeline uses a language model like GPT-4 with multimodal capabilities, incorporating the images and text retrieved from the document store.

### Additional Considerations

- **Chunking Strategy**: Using by-title chunking allows for more cohesive and related chunks of data, making retrieval more meaningful.
- **Base64 Conversion**: Images are converted to Base64 format so that they can be sent as context to language models.
- **Using Multimodal Models**: GPT-4 (or alternatives) are capable of understanding both visual and textual information, which is crucial for generating responses that integrate all components of a PDF.

### Conclusion

This tutorial effectively demonstrates how to build a PDF chatbot that considers various media elements such as images, tables, and text. The overall process involves parsing with "Unstructured," summarizing with multimodal language models, storing in vector/document databases, and retrieving content for a meaningful response.

You now have a detailed understanding of the entire process along with code examples to get started. If you have specific elements you'd like to focus on more or require further clarification, let me know!

[[RAG]]  [[Chatbots]]  [[LangChain]]  [[Python]]