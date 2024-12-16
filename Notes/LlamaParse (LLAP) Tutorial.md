---
Video-URL: https://www.youtube.com/watch?v=dTVjx1kEJrc&list=WL&index=4
tags:
- llamaindex
- python
---

## **LlamaParse (LLAP) Tutorial**

Detailed Summary of LLAP Parse Demonstration by Lri Devell at LlamaIndex

In this comprehensive summary, we delve into a demonstration by **Lri Devell** from **LlamaIndex** showcasing the features and usage of **LLAP Parse**, an industry-leading PDF and document parser. The demonstration highlights how LLAP Parse simplifies handling complex documents, such as insurance policies, by converting dense text into easily understandable summaries using Large Language Models (LLMs).

## Introduction

**LLAP Parse** is a powerful tool integrated into **LlamaIndex** that offers robust parsing capabilities for PDFs and various other document types. Designed to be user-friendly, LLAP Parse leverages APIs to transform complex documents into structured formats, making them more accessible and easier to analyze using LLMs like OpenAI's GPT models.

## Features of LLAP Parse

- **Industry-Leading PDF Parsing:** Efficiently handles complex PDF documents, extracting text, tables, and other essential elements.
- **Support for Multiple Document Types:** Beyond PDFs, LLAP Parse can parse various document formats, catering to diverse needs.
- **Seamless API Integration:** Easily integrates with LlamaIndex through simple API calls, streamlining the parsing process.
- **Enhanced [[LLM]] Compatibility:** Converts dense text into markdown and structured lists, facilitating better understanding and interaction with LLMs.

## Getting Started with LLAP Parse

### Installation

To begin using LLAP Parse, install the necessary packages using `pip`. You'll need to install both `llama-index` and `llama-parse` as separate packages.

```bash
pip install llama-index llama-parse
```

### API Key Setup

LLAP Parse requires two API keys:

1. **OpenAI API Key:** Needed for parsing functionalities.
2. **Llama Cloud API Key:** Obtainable from LlamaIndex Cloud.

Ensure you have both API keys ready before proceeding.

## Parsing a Complex PDF Document

### Downloading the PDF

For demonstration purposes, a complex insurance policy PDF from **Iridia** is used. This document contains numerous clauses, exclusions, and coverage details, making it an excellent candidate to showcase LLAP Parse's capabilities.

```Python
import requests

# URL of the insurance policy PDF
pdf_url = "https://example.com/iridia_insurance_policy.pdf"

# Download the PDF
response = requests.get(pdf_url)
with open("iridia_insurance_policy.pdf", "wb") as file:
    file.write(response.content)
```

### Initializing Asynchronous Components

LLAP Parse operates asynchronously to ensure efficient processing within notebooks.

```Python
import asyncio

# Initialize asynchronous components
async def initialize():
    # Initialization logic if any
    pass

# Run the initialization
asyncio.run(initialize())
```

### Parsing the PDF

Using LLAP Parse to convert the downloaded PDF into markdown format.

```Python
import llama_parse

# Specify desired result type
result_type = "markdown"

# Path to the downloaded PDF
pdf_path = "iridia_insurance_policy.pdf"

# Parse the PDF
parsed_markdown = llama_parse.parse(file_path=pdf_path, result_type=result_type)

# Display the parsed markdown
print(parsed_markdown)
```

**Output:** The output will be the exact text from the PDF converted into markdown format, making it more readable and easier for LLMs to process.

## Processing Parsed Data

### Converting to Markdown

LLAP Parse first converts the PDF into markdown, preserving the document's structure and content without alterations.

### Breaking Down into Text and Tables

To enhance comprehension, especially for documents laden with tables, the markdown is further parsed into distinct text and table elements.

```Python
from llama_index.node_parser import MarkdownElementNodeParser

# Initialize the Markdown parser
parser = MarkdownElementNodeParser()

# Parse the markdown into nodes
nodes = parser.parse(parsed_markdown)

# Extract tables and text
text_nodes = [node for node in nodes if node.type == "text"]
table_nodes = [node for node in nodes if node.type == "table"]
```

### Creating a Vector Store Index

The extracted nodes are then stored in a vector store index, facilitating efficient querying.

```Python
from llama_index import VectorStoreIndex

# Create a vector store index from the nodes
vector_store_index = VectorStoreIndex(nodes=text_nodes + table_nodes)
```

### Building a Query Engine

A query engine is established from the vector store index to handle user queries.

```Python
from llama_index import QueryEngine

# Initialize the query engine
query_engine = vector_store_index.as_query_engine()
```

## Enhancing Query Results with Parser Instructions

### Initial Query and Limitations

A sample query is executed against the basic setup to determine coverage details.

```Python
# Sample query
query = "My trip was delayed and I paid $45. How much am I covered for?"

# Execute the query
response = query_engine.query(query)
print(response)
```

**Output:**

```
You are covered for the amount mentioned in the Certificate of Insurance.
```

_Limitation:_ The response is vague and doesn't provide specific coverage details.

### Using Parser Instructions for Improved Understanding

To address the limitation, parser instructions are provided to LLAP Parse to transform the document into a list of covered and non-covered items, enhancing the LLM's comprehension.

```Python
# Define parser instructions
parser_instructions = """
Read this insurance policy document and extract a list of items that are covered and not covered. Present the information in a clear, structured list format.
"""

# Parse the PDF with instructions
parsed_list = llama_parse.parse(
    file_path=pdf_path,
    result_type="markdown",
    instructions=parser_instructions
)

# Display the parsed list
print(parsed_list)
```

**Output:**

```
**Covered:**
- Trip delays up to $45

**Not Covered:**
- Baby food
```

### Comparative Query Results

Re-executing the initial query using the enhanced parsed data yields more precise answers.

```Python
# Create a new query engine with the parsed list
enhanced_vector_store_index = VectorStoreIndex(nodes=[parsed_list])
enhanced_query_engine = enhanced_vector_store_index.as_query_engine()

# Execute the same query
enhanced_response = enhanced_query_engine.query(query)
print(enhanced_response)
```

**Enhanced Output:**

```
You are covered for the trip delay amount you paid, which is $45.
```

**Additional Queries:**

1. **Query:** "I just had a baby. Is baby food covered?"

    **Vanilla Response:** _(Unhelpful or no information)_

    **Enhanced Response:**

    ```
    Baby food is not covered under the insurance policy.
    ```

2. **Query:** "Do you mention in your insurance policy how is gauze in your operation covered?"

    **Vanilla Response:**

    ```
    It's covered as part of your surgical tool procedure. (Detailed explanation)
    ```

    **Enhanced Response:**

    ```
    Procedure charges cover the use of gauze in your operation.
    ```

_Conclusion:_ Providing parser instructions enables LLAP Parse to structure the data in a manner that facilitates precise and relevant responses from the LLM.

## Conclusion

LLAP Parse, integrated with LlamaIndex, offers a streamlined solution for parsing complex documents like insurance policies. By converting dense text into structured formats such as markdown and lists, it enhances the ability of Large Language Models to understand and interact with the content effectively. This capability not only simplifies document management but also empowers users to extract precise information effortlessly.

## References and Useful Links

- **LlamaIndex:** [https://llamaindex.ai](https://llamaindex.ai)
- **LLAP Parse Documentation:** [https://llamaindex.ai/docs/llama-parse](https://llamaindex.ai/docs/llama-parse)
- **OpenAI:** [https://openai.com](https://openai.com)
- **LlamaIndex Cloud API Keys:** [https://cloud.llamaindex.ai](https://cloud.llamaindex.ai)

## Complete Code Example

Below is the complete Python code example based on the demonstration:

```Python
# Install necessary packages
!pip install llama-index llama-parse

# Import required libraries
import asyncio
import requests
import llama_parse
from llama_index.node_parser import MarkdownElementNodeParser
from llama_index import VectorStoreIndex

# Define asynchronous initialization
async def initialize():
    # Placeholder for any asynchronous setup
    pass

# Run the asynchronous initialization
asyncio.run(initialize())

# Download the insurance policy PDF
pdf_url = "https://example.com/iridia_insurance_policy.pdf"
response = requests.get(pdf_url)
with open("iridia_insurance_policy.pdf", "wb") as file:
    file.write(response.content)

# Set API keys
import os
os.environ["OPENAI_API_KEY"] = "your_openai_api_key_here"
os.environ["LLAMA_CLOUD_API_KEY"] = "your_llama_cloud_api_key_here"

# Parse the PDF into markdown
result_type = "markdown"
pdf_path = "iridia_insurance_policy.pdf"
parsed_markdown = llama_parse.parse(file_path=pdf_path, result_type=result_type)
print("Parsed Markdown:\n", parsed_markdown)

# Initialize the Markdown parser
parser = MarkdownElementNodeParser()
nodes = parser.parse(parsed_markdown)

# Extract text and table nodes
text_nodes = [node for node in nodes if node.type == "text"]
table_nodes = [node for node in nodes if node.type == "table"]

# Create a vector store index
vector_store_index = VectorStoreIndex(nodes=text_nodes + table_nodes)

# Build the query engine
query_engine = vector_store_index.as_query_engine()

# Execute a sample query
query = "My trip was delayed and I paid $45. How much am I covered for?"
response = query_engine.query(query)
print("Vanilla Response:\n", response)

# Define parser instructions for enhanced parsing
parser_instructions = """
Read this insurance policy document and extract a list of items that are covered and not covered. Present the information in a clear, structured list format.
"""

# Parse the PDF with instructions
parsed_list = llama_parse.parse(
    file_path=pdf_path,
    result_type="markdown",
    instructions=parser_instructions
)
print("Parsed List:\n", parsed_list)

# Create an enhanced vector store index
enhanced_vector_store_index = VectorStoreIndex(nodes=[parsed_list])

# Build the enhanced query engine
enhanced_query_engine = enhanced_vector_store_index.as_query_engine()

# Execute the same query with the enhanced engine
enhanced_response = enhanced_query_engine.query(query)
print("Enhanced Response:\n", enhanced_response)

# Additional queries
additional_queries = [
    "I just had a baby. Is baby food covered?",
    "Do you mention in your insurance policy how is gauze in your operation covered?"
]

for q in additional_queries:
    resp = enhanced_query_engine.query(q)
    print(f"Query: {q}\nResponse: {resp}\n")
```

**Note:** Replace `"your_openai_api_key_here"` and `"your_llama_cloud_api_key_here"` with your actual API keys.

[[LLM Frameworks]] | [[LLM]] | [[Python]]
