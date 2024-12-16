---
github_link: https://github.com/jbarrasa/goingmeta
tags:
- graph
- rag
- python
video-url: https://www.youtube.com/watch?v=UmP0pFFsMsE&list=WL&index=2
---

## **Ontology-driven end-to-end GraphRAG

### Detailed Overview and Instructions: Knowledge Graph Construction and RAG with the GraphRag Python Library

#### **Introduction**

This episode covers an advanced walkthrough of building and interacting with knowledge graphs using the **GraphRag Python Library**. Three primary use cases are discussed:

1. **Knowledge Graph Construction**
2. **Entity Resolution**
3. **Retrieval-Augmented Generation (RAG)** using both vector and text-to-Cypher strategies.

The examples center around a dataset of artworks and artists, leveraging ontologies to guide graph construction, data deduplication, and natural language question answering.

---

#### **Key Concepts**

1. **Ontology-Driven Design:**
   - Ontologies formalize relationships between data entities.
   - Ontology elements (classes, properties, and relationships) define how data is structured and queried.
   - Example used: A simple ontology for artists, artworks, and their relationships.

2. **GraphRag Library Features:**
   - Automates knowledge graph creation from unstructured data.
   - Provides tools for entity extraction, deduplication, and retrieval.
   - Supports both vector-based and Cypher-based retrieval methods.

3. **Steps in the Workflow:**
   - **Data Ingestion and Chunking:** Splits unstructured text for embedding.
   - **Entity Extraction:** Identifies entities and relationships using LLMs.
   - **Entity Resolution:** Merges duplicate nodes in the graph.
   - **Question Answering:** Retrieves and generates answers using graph data.

---

#### **Step-by-Step Instructions**

##### **1. Knowledge Graph Construction**

- **Setup:**
  - Initialize a Neo4j database.
  - Use a pre-defined ontology (e.g., RDF in Turtle format) to define graph schema.

```python
from graph_rag import KnowledgeGraphBuilder

# Step 1: Configure Database Connection
neo4j_driver = KnowledgeGraphBuilder(
    uri="bolt://localhost:7687",
    user="neo4j",
    password="password"
)

# Step 2: Define Ontology
ontology_path = "art_ontology.ttl"

# Parse ontology into schema for GraphRag
schema = ontology_to_schema(ontology_path)

# Step 3: Initialize Pipeline
pipeline = KnowledgeGraphBuilder(
    driver=neo4j_driver,
    ontology_schema=schema,
    chunk_size=2500,  # Configure chunking
    overlap=100,
    embedder_service="openai-embedding"
)

# Step 4: Process Data Files
for file in os.listdir("./data"):
    if file.endswith(".txt"):
        pipeline.run_pipeline(input_file=f"./data/{file}")
```

- **Result:**
  - The graph is populated with two layers:
    - **Lexical Layer:** Represents document chunks with embeddings.
    - **Domain Layer:** Represents extracted entities (e.g., artists, artworks).

---

##### **2. Entity Resolution**

- **Goal:** Merge duplicate nodes (e.g., "David Hockney" and "Hockney, David") based on shared properties.
- **Using Ontology for Primary Keys:**
  - Define `inverse functional properties` in the ontology to indicate unique identifiers.

```ttl
:ProfessionalName a owl:InverseFunctionalProperty ;
    rdfs:domain :Artist ;
    rdfs:range xsd:string .

:ArtworkKnownAs a owl:InverseFunctionalProperty ;
    rdfs:domain :Artwork ;
    rdfs:range xsd:string .
```

- **Resolution Script:**

```python
from graph_rag import EntityResolver

# Step 1: Extract Primary Keys from Ontology
primary_keys = extract_primary_keys_from_ontology(ontology_path)

# Step 2: Configure Resolver
resolver = EntityResolver(driver=neo4j_driver)

# Step 3: Run Deduplication
for key in primary_keys:
    resolver.resolve_duplicates(property=key)
```

- **Result:**
  - Nodes sharing the same primary key (e.g., `ProfessionalName`) are merged.
  - Reduces redundancy in the graph.

---

##### **3. Retrieval-Augmented Generation (RAG)**

- **Vector-Based Retrieval:**
  - Embeds questions and finds matching chunks using cosine similarity.

```python
from graph_rag import VectorRetriever

# Step 1: Configure Vector Retriever
retriever = VectorRetriever(
    driver=neo4j_driver,
    embedder_service="openai-embedding"
)

# Step 2: Ask Questions
question = "Who painted 'La Femme en Bleu'?"
result = retriever.query(question=question, top_k=3)
print(result)
```

- **Text-to-Cypher Retrieval:**
  - Converts natural language questions into Cypher queries.

```python
from graph_rag import TextToCypherRetriever

# Step 1: Configure Cypher Retriever
cypher_retriever = TextToCypherRetriever(
    driver=neo4j_driver,
    schema=ontology_to_schema(ontology_path)
)

# Step 2: Ask Questions
question = "Who painted 'La Femme en Bleu'?"
result = cypher_retriever.query(question=question)
print(result)
```

- **Result:**
  - Answers retrieved from graph using generated Cypher queries.
  - Example output: `Pablo Picasso painted 'La Femme en Bleu'.`

---

#### **Additional Notes**

1. **Error Handling:**
   - Ensure the database connection is stable.
   - Handle cases where chunks or entities are missing.

2. **Ontology Tools:**
   - Use editors like **Protégé** or **WebProtégé** to manage and export ontologies.

3. **Extensibility:**
   - Extend the pipeline for additional entity types.
   - Incorporate external ontologies like Getty AAT for domain-specific terms.

---

#### **Conclusion**

This guide demonstrates how to use the GraphRag library to construct, refine, and query knowledge graphs efficiently. By leveraging ontologies, the process becomes more structured, scalable, and adaptable to various domains. Explore the provided code on GitHub for hands-on practice and extend it to your datasets and ontologies.

[[Graphs]]   [[RAG]]   [[Python]]