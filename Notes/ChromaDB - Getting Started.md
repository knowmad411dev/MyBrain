---
tags:
- database
- python
- chromadb
---

# ChromaDB - Getting Started

## Summary of ChromaDB Usage for Semantic Search with Python

This guide provides a step-by-step walkthrough of using [ChromaDB](https://www.trychroma.com/), an open-source vector database for handling embeddings and performing semantic search in Python. The example focuses on improving a restaurant menu search functionality by implementing semantic search capabilities.

### Table of Contents

1. Introduction
2. Installing ChromaDB
3. Creating a ChromaDB Client and Collection
4. Adding Data to the Collection
5. Performing Semantic Search
6. Including Embeddings in the Search Results
7. Implementing Semantic Search on a Restaurant Menu
8. Loading Data from a CSV File
9. Deleting and Recreating the Collection
10. Switching to a Better Embedding Model
11. Installing `sentence_transformers`
12. Testing the Improved Semantic Search
13. Persisting the Database to Disk
14. Conclusion
15. Additional Resources

### Introduction

**ChromaDB** is an open-source vector database that simplifies storing and querying embeddings. It's particularly useful for applications like semantic search, where you want to find items that are semantically similar to a query, rather than just matching keywords.

### Installing ChromaDB

First, install ChromaDB using `pip`:

```bash
pip install chromadb
```

### Creating a ChromaDB Client and Collection

To use ChromaDB, start by creating a client and a collection:

```python
import chromadb
client = chromadb.Client()
collection = client.create_collection('menu_items')
```

### Adding Data to the Collection

Add some menu items to the collection:

```python
data = [
    {'id': '1', 'content': 'Grilled Chicken Salad'},
    {'id': '2', 'content': 'Spaghetti Carbonara'},
    {'id': '3', 'content': 'Shrimp Tacos'},
    {'id': '4', 'content': 'Cheeseburger'},
    {'id': '5', 'content': 'Margherita Pizza'}
]

for item in data:
    collection.add(item['id'], item['content'])
```

### Performing Semantic Search

Perform a semantic search by querying the collection for items similar to a search term:

```python
query = 'seafood'
results = collection.query(query, n_results=3)

for result in results:
    print(result)
```

### Including Embeddings in the Search Results

Use sentence transformers to generate embeddings and include them in the collection:

```python
from sentence_transformers import SentenceTransformer
model = SentenceTransformer('all-MiniLM-L6-v2')

embeddings = [model.encode(item['content']) for item in data]
for i, embedding in enumerate(embeddings):
    collection.update_embedding(data[i]['id'], embedding)
```

### Implementing Semantic Search on a Restaurant Menu

For our restaurant menu example, we can use the query to find dishes related to a specific ingredient or type of cuisine:

```python
query = 'spicy shrimp'
results = collection.query(query, n_results=5)
for result in results:
    print(result)
```

### Persisting the Database to Disk

By default, ChromaDB operates in memory. To persist the database to disk, specify a `persist_directory` when creating the client:

```python
from chromadb.config import Settings

client = chromadb.Client(Settings(
    chroma_db_impl="duckdb+parquet",
    persist_directory="vector_db"  # Folder to store the database
))
```

After adding data to the collection, you can persist it:

```python
client.persist()
```

This creates a folder named `vector_db` containing the persisted database.

### Conclusion

By following these steps, you can implement semantic search functionality using ChromaDB in your application. This enhances the user experience by returning semantically relevant results, even when search terms don't exactly match item names.

### Additional Resources

- **ChromaDB**: [GitHub Repository](https://github.com/chroma-core/chroma)
- **Sentence Transformers**: Pretrained Models
- **OpenAI Embeddings**: [Documentation](https://platform.openai.com/docs/guides/embeddings)

[[ChromaDB]]  [[Vector Databases]]  [[Python]]