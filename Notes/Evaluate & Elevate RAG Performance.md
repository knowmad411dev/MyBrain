---
tags:
- rag
- llamaindex
- python
---
## **Evaluate & Elevate RAG Performance

Retrieval Augmented Generation (RAG) systems are popular, combining information retrieval with the power of generative large language models. Achieving high performance in production settings is challenging and requires careful development, logging, evaluation, and iteration.

In this series of two — _human-generated ;)_ — posts, we will dive into key aspects of evaluating a RAG system in both the development phase (pre-production) and in-production. Pre-production evaluation is done during development and iteration, focusing on hallucination, conciseness, helpfulness, context relevancy, answer similarity, and more. Evaluation can be conducted by AI (LLM-as-a-judge) or human evaluators (domain experts). In production, additional evaluation can be based on implicit and explicit feedback from end-users.

This first post focuses on pre-production evaluation, demonstrating how to use three powerful tools to build and evaluate a RAG system: [LlamaIndex](https://www.llamaindex.ai/) for building a simple RAG system, [Ragas](https://ragas.io/) as an evaluation framework, and [Literal AI](https://literalai.com/) as a visual and interactive interface to aid evaluation.

### What’s in this Post:

1.  Initial Setup & Dataset
2.  Build a Simple RAG System with LlamaIndex
3.  Evaluate RAG System with Ragas
4.  Analyze Evaluation Results in Literal AI

### 1. Initial Setup

In this tutorial, we will use LlamaIndex, OpenAI, Ragas, and LiteralAI, requiring the installation of the following libraries:

```python
!pip install llama-index
!pip install ragas
!pip install literalai
!pip install python-dotenv
```

For both [OpenAI](https://platform.openai.com/api-keys) (billed) and [Literal AI](https://docs.literalai.com/get-started/installation#how-to-get-my-api-key) (free), you need an API key. Store these in your environment variables or in an `.env` file.

We will initiate Literal AI to instrument the LlamaIndex application, using Literal AI later to view chat logs and evaluation results.

```python
import os
from literalai import LiteralClient
from dotenv import load_dotenv

load_dotenv()

literalai_client = LiteralClient(api_key=os.getenv("LITERAL_API_KEY"))
literalai_client.instrument_llamaindex()
```

Download the [Podcast transcripts from Kaggle](https://www.kaggle.com/datasets/harrywang/acquired-podcast-transcripts-and-rag-evaluation) and store them in a `/data` folder. This dataset will provide questions and human answers for evaluation.

### 2. Build a Simple RAG System with LlamaIndex

[LlamaIndex](https://www.llamaindex.ai/) is a framework to build RAG applications. In this example, we use several components:

1. **Embedding Model**: LlamaIndex uses OpenAI’s text-embedding-ada-002 model by default to create vector embeddings for the data.
2. **LLM Model**: Generates answers based on input (using OpenAI's gpt-3.5-turbo by default).
3. **Document Loader**: Reads documents from a source into the application. We use [SimpleDirectoryReader](https://docs.llamaindex.ai/en/stable/module_guides/loading/simpledirectoryreader/).
4. **Indexing and Storing**: Uses an in-memory vector store by default.
5. **Prompt Template**: Default prompts are used to guide the LLM.
6. **Query Engine**: Interface to ask questions of the indexed data.

```python
from llama_index.core import VectorStoreIndex, SimpleDirectoryReader

documents = SimpleDirectoryReader("data/acquired-individual-transcripts/acquired-individual-transcripts").load_data()
index = VectorStoreIndex.from_documents(documents, show_progress=True)
```

We build a query engine from this index using a default prompt by LlamaIndex. By default, the query engine retrieves 2 data chunks, but we change this to retrieve 1 chunk only.

```python
query_engine = index.as_query_engine(similarity_top_k=1)
```

We now have a simple RAG system! We indexed documents and built a query engine that retrieves 1 chunk of data and generates an answer. Here is an example query:

```python
response = query_engine.query("What boots and jacket we often see Jeff Bezos in?")
print(response)
```

Since we instrumented this RAG application, we can view this query, the retrieval steps, and response on the [Literal AI platform](https://cloud.getliteral.ai/).

### 3. Evaluate RAG System with Ragas

For evaluation, we use [Ragas](https://docs.ragas.io/en/stable/index.html), a Python framework for RAG evaluation that integrates well with LlamaIndex. We will evaluate our RAG system using two key areas:

- **Retrieval Evaluation**: Metrics like **Context Precision**, **Context Recall**, and **Mean Reciprocal Rank (MRR)**.
- **Response Evaluation**: Metrics like **Faithfulness**, **Answer Relevancy**, **Noise Sensitivity**, and **Correctness**.

First, create an evaluation dataset in Literal AI:

```python
import csv

DATASET_NAME = "Podcast Evaluation Dataset"
literal_dataset = literalai_client.api.create_dataset(name=DATASET_NAME)

with open('data/qa-evaluation.csv', newline='', encoding='ISO-8859-1') as csvfile:
    evaluation_data = csv.reader(csvfile, delimiter=',')
    next(evaluation_data, None)
    for row in evaluation_data:
        literal_dataset.create_item(
            input={"content": row[0]},
            expected_output={"content": row[1]}
        )
```

Transform the dataset to a format that Ragas can use:

```python
experiment_items = literal_dataset.items
questions, ground_truths = [], []

for item in experiment_items:
    question = item.input["content"]
    ground_truth = item.expected_output["content"]
    questions.append(question)
    ground_truths.append(ground_truth)

from datasets import Dataset

data_samples = {'question': questions, 'ground_truth': ground_truths}
data_samples_set = Dataset.from_dict(data_samples)
```

Run the Ragas experiment with basic evaluation metrics:

```python
from ragas.metrics import answer_relevancy, context_precision, context_recall
from llama_index.llms.openai import OpenAI
from llama_index.embeddings.openai import OpenAIEmbedding
from ragas.integrations.llama_index import evaluate

metrics = [answer_relevancy, context_precision, context_recall]
evaluator_llm = OpenAI(model="gpt-3.5-turbo")

result = evaluate(
    query_engine=query_engine,
    metrics=metrics,
    dataset=data_samples_set,
    llm=evaluator_llm,
    embeddings=OpenAIEmbedding(),
)
```

### 4. Analyze Evaluation Results in Literal AI

```python
result = result.to_pandas()
experiment = literal_dataset.create_experiment(
    name="Experiment 1 - Top 1 retrieval",
    params=[{"top_k": 1}]
)

for i, row in result.iterrows():
    scores = [
        {"name": answer_relevancy.name, "type": "AI", "value": row[answer_relevancy.name]},
        {"name": context_precision.name, "type": "AI", "value": row[context_precision.name]},
        {"name": context_recall.name, "type": "AI", "value": row[context_recall.name]},
    ]
    experiment_item = {
        "datasetItemId": experiment_items[i].id,
        "scores": scores,
        "input": {"question": row["question"]},
        "output": {"content": row["answer"]},
    }
    experiment.log(experiment_item)
```

You now have experiment results in Literal AI. The summary of the experiment, along with individual items, can be reviewed. Comparing experiments provides insights into areas of improvement.

[[RAG]]  [[LlamaIndex Framework]]  [[Python]]