---
Video-URL: https://youtu.be/8BV9TW490nQ
tags:
- langchain
---

## **LangChain

LangChain is an open-source framework that simplifies the development of applications using large language models (LLMs). It provides a unified interface for interacting with various LLMs, making building chatbots, question-answering systems, and other AI-powered applications easier.

In this tutorial, I'll teach you LangChain in 7 easy steps. You will learn the core features of the framework and we will cover:

-   Why you want to learn LangChain
-   Composing chains with prompt templates and loaders
-   The runnable protocol and LangChain expression language
-   Creating vectorstore-backed retrievers
-   Building RAG chains
-   Using tools with chains
-   Building agents with access to tools

By the end of the tutorial, you will have a solid foundation for diving deeper into the LangChain ecosystem and start testing, deploying, and building advanced Multi Agent systems with [[LangGraph]].

### Colab Notebook & Interactive Map

The Colab notebook is [available here](https://colab.research.google.com/drive/1BGEPkjNxnW2U8FC-NiKtSCrt11g6TS4Q?usp=sharing&ref=rabbitmetrics.com) and the interactive LangChain map is [available here.](https://xmind.app/m/4iEV2x?ref=rabbitmetrics.com)

## 1\. LangChain Overview

LangChain is an open-source framework for developing applications with large language models (LLMs). It enables developers to integrate LLMs with external sources of computation and data, streamlining the creation of sophisticated AI applications. LangChain simplifies the deployment of LLM applications by providing essential tools for inspection, monitoring, and evaluation, although this tutorial focuses on the core library.

![[7f066c6c8440dfae640a11ac46452ad0_MD5.jpg]]

LangChain allows users to query data by retrieving relevant context from vector databases. This approach enhances the LLM's ability to provide accurate and contextually relevant responses. Additionally, LangChain supports creating agent systems by combining LLMs with various tools, allowing for complex interactions and functionalities.

### Types of Applications

Applications developed with LangChain generally fall into three categories:

1.  **[[Chatbots]]**: Enhanced with LLMs for more intelligent marketing, customer support, and education interactions.
2.  **Retrieval-Augmented Generation ([[RAG]]) Q&A**: Used for summarizing large documents, data analysis, and generating code by referencing external sources.
3.  **Agent Systems** involve multi-agent setups and human interactions, utilizing LangGraph for complex workflows. They are applicable in areas like supply chain management and operations optimization.

### Why Learn LangChain?

There are at least two compelling reasons to learn LangChain:

**Transition to Natural Language Programming:** LangChain facilitates the transition to natural language as the highest level of programming. This shift enables users to write executable code using natural language inputs, making programming more accessible.

![[75dee5e1948a0b9173863f0be8dd0674_MD5.jpg]]

Programming Language Hierarchies

By leveraging LLMs, developers can create complex applications without traditional coding, streamlining workflows and enhancing productivity. This evolution represents a significant step in programming, as it allows users to focus on problem-solving rather than syntax, ultimately broadening the scope of who can develop software.

LangChain enables the creation of pipelines that transform natural language into executable programs. By leveraging these chains, users can input natural language and receive valuable outputs such as reports, analyses, or computer programs.

This capability is powered by the current generation of advanced LLMs, which can produce functioning code. This transformation is not a distant future concept—it's available today, making programming more accessible and efficient for a broader audience.

**Innovations with LangGraph**: LangGraph, built on LangChain, offers powerful capabilities for creating complex interactions between agents and humans. This functionality is essential for large organizations where secure access to files and data is crucial.

![[bceaf915fd138f79193169a5a6ed96fe_MD5.jpg]]

LangGraph also supports the development of multi-agent systems, similar to Autogen and CrewAI. These systems enable asynchronous communication and task division among specialized agents, enhancing efficiency and scalability across various applications. This flexibility supports a divide-and-conquer approach, where agents can operate independently or collaboratively, depending on the requirements. This is particularly useful in scenarios where a single LLM cannot handle all tasks, enabling specialized agents to manage specific functions.

### Installing Libraries and Connecting to LLMs

To get started with LangChain in a Colab notebook, first install the necessary libraries:

```python
!pip install -qU python-dotenv langchain langchain-community openai anthropic langchain-openai langchain-anthropic
```

Installing the necessary packages using pip, including `python-dotenv`, `langchain`, `langchain-community`, `openai`, `anthropic`, `langchain-openai`, and `langchain-anthropic` . We load the API keys from a .env file and connect.

```python
from dotenv import load_dotenv load_dotenv() from langchain_anthropic import ChatAnthropic llm_claude3 = ChatAnthropic(model='claude-3-opus-20240229') from langchain_openai import ChatOpenAI llm_gpt4 = ChatOpenAI(model="gpt-4o") llm_claude3.invoke("What is LangChain?").content
```

Load the API keys from a .env file and connect to the OpenAI and Anthropic APIs. We create instances of the ChatOpenAI and ChatAnthropic classes, specifying the desired models. We invoke a simple query using the llm\_claude3 instance to verify the setup.

```python
system_prompt=""" You explain things to people like they are five year olds. """ user_prompt=f""" What is LangChain? """ from langchain_core.messages import HumanMessage, SystemMessage import textwrap messages = [ SystemMessage(content=system_prompt), HumanMessage(content=user_prompt), ] response=llm_gpt4.invoke(messages) answer = textwrap.fill(response.content, width=100) print(answer)
```

We are making a basic request using system and human/user messages. We define a system prompt instructing the LLM to explain things like talking to a five-year-old and a user prompt asking, "What is LangChain?".

We create instances of the SystemMessage and HumanMessage classes, pass them to the `.invoke()` Method and print the wrapped response.

## 2\. Chains, Prompts and Loaders

Let's dive into chains, prompts, and loaders, and build our first chain. A chain in LangChain is a sequence of interconnected components that process a user's query, utilizing one or more LLMs to generate and deliver valuable output.

![[e0a441044def54779cb6a9efab982f4a_MD5.jpg]]

### Understanding Chains

Think of a chain as a pipeline in the world of LLMs. It processes input queries and transforms them into useful outputs, such as answers, document summaries, recommendations, insights, executable code, or JSON for API calls. By automating this process, chains provide significant value.

### Components of a Chain

The components of a chain typically include:

-   **Prompts**: Templates that guide the LLM's responses.
-   **LLMs or Chat Models**: The engines that generate responses based on the prompts.
-   **Output Parsers**: Tools that parse the LLM's output.
-   **Tools**: Extensions that allow LLMs to extract additional information from APIs or run code, turning LLMs into agents.
-   **General Functions**: Additional functionalities that can be chained together.

In LangChain, these components, known as runnables, can be combined to form a comprehensive pipeline.

### An Analogy: Data Pipelines

An LLM chain is similar to a data pipeline. In a data pipeline, raw data is transformed into clean, structured data. Similarly, in an LLM chain, a query is transformed into valuable output using LLM calls, functions, and additional data.

![[40bc40ed097eea612c90ca7b712f6065_MD5.jpg]]

### Automation and Deployment

LangChain not only helps you build chains but also allows you to test, deploy, monitor, and evaluate them. This can be automated with continuous integration and continuous deployment (CI/CD) processes using LangSmith and LangServe, enhancing efficiency and reliability in your LLM applications.

### Building a Chain with Prompt and Loaders

In this section, we'll explore how to create chains using LangChain, focusing on prompts and loaders.

```python
from langchain.prompts import PromptTemplate prompt_template = """ You are a helpful assistant that explains AI topics. Given the following input: {topic} Provide an explanation of the given topic. """ prompt = PromptTemplate( input_variables=["topic"], template=prompt_template, ) chain = prompt | llm_gpt4 chain.invoke({"topic":"What is LangChain"}).content
```

This code defines a prompt template where the AI explains topics based on user input. The `{topic}` The user's query is replaced in the variable. We create a chain by connecting the prompt template to the GPT-4 model using the pipe operator. This setup allows us to process the user's input and generate a response.

To create a more advanced chain, we'll transcribe a YouTube video using LangChain. First, install the YouTube Transcript API. Then, import the YouTube Loader from LangChain's community document loaders. By passing a video URL to the loader, you can extract the transcript, which is returned as a list of documents. To obtain the raw transcript, simply extract the page content from these documents, or pass the documents directly to the chain.

```python
! pip install --upgrade --quiet youtube-transcript-api from langchain_community.document_loaders import YoutubeLoader loader = YoutubeLoader.from_youtube_url( "https://www.youtube.com/watch?v=AOEGOhkGtjI", add_video_info=False ) docs=loader.load() transcript=docs[0].page_content
```

Now, let's set up a chain that summarizes YouTube videos given a transcript. We inject the video transcript into the prompt template as the input variable and then set up the chain using the pipe operator. By invoking it with the video transcript, you can get a concise summary without manually extracting the raw text.

```python
prompt_template = """ You are a helpful assistant that explains YT videos. Given the following video transcript: {video_transcript} Give a summary. """ prompt = PromptTemplate( input_variables=["video_transcript"], template=prompt_template, ) chain = prompt | llm_gpt4 chain.invoke({"video_transcript":docs}).content
```

## 3\. LangChain Expression Language (LCEL)

LangChain Expression Language (LCEL) simplifies building complex chains from basic components. It uses the pipe operator (`|`) to chain different components, feeding the output from one element to the next. A simple example of a chain composed this way would be a prompt combined with a model and an output parser.

These components are called "runnables". Think of LCEL as a declarative way of composing these runnables into chains. Here's a step-by-step example of what a basic chain looks like:

1.  Input to the chain (typically a dictionary)
2.  Input is sent to a prompt
3.  Prompt value is sent to the LLM or chat model
4.  Chatmodel returns a chat message
5.  The parser extracts a string from the chat message
6.  A string is the output of the chain

![[f3fa6e70bf1f74f27eea2db00750bbfe_MD5.jpg]]

LangChain allows multiple chains to be chained together in this manner.

### The Runnable Protocol

A runnable is a unit of work that can be invoked, batched, streamed, transformed, and composed. The chains we build with LangChain and their components are runnables. We can also pass arbitrary functions into a chain, which will be converted into runnables.

Core runnable objects in LangChain:

1.  **RunnableSequence**: Chains together multiple runnable components, ensuring each component processes its input and passes its output to the next component.
2.  **RunnableLambda**: Turns a Python callable (like a function) into a runnable component, allowing integration of arbitrary functions into chains.
3.  **RunnablePassthrough**: Either passes its input through unchanged or adds additional keys to the output. It can act as a placeholder or allow flexible integrations into sequences.
4.  **RunnableParallel**: Runs multiple runnables concurrently, allowing branching where two chains run on the same input but return different outputs.

Let's look at some code examples to see how these work in practice:

```python
from langchain.prompts import PromptTemplate from langchain_core.output_parsers import StrOutputParser summarize_prompt_template = """ You are a helpful assistant that summarizes AI concepts: {context} Summarize the context """ summarize_prompt = PromptTemplate.from_template(summarize_prompt_template) output_parser = StrOutputParser() chain = summarize_prompt | llm_gpt4 | output_parser result = chain.invoke({"context": "What is LangChain?"}) print(result) print(type(chain)) # Should print <class 'langchain_core.runnables.base.RunnableSequence'>
```

This example creates a simple chain using the pipe operator. The chain is of type `RunnableSequence`.

Now, let's look at using a `RunnableLambda`:

```python
from langchain_core.runnables import RunnableLambda summarize_chain = summarize_prompt | llm_gpt4 | output_parser length_lambda = RunnableLambda(lambda summary: f"Summary length: {len(summary)} characters") lambda_chain = summarize_chain | length_lambda result = lambda_chain.invoke({"context": "What is LangChain?"}) print(result) print(type(lambda_chain.steps[-1])) # Should print <class 'langchain_core.runnables.base.RunnableLambda'>
```

We can also use a function in a chain without explicitly converting it to a `RunnableLambda`:

```python
chain_with_function = summarize_chain | (lambda summary: f"Summary length: {len(summary)} characters") print(type(chain_with_function.steps[-1])) # Still a RunnableLambda result = chain_with_function.invoke({"context": "What is LangChain?"}) print(result)
```

Here's an example of using `RunnablePassthrough` as a placeholder:

```python
from langchain_core.runnables import RunnablePassthrough passthrough = RunnablePassthrough() placeholder_chain = summarize_chain | passthrough | length_lambda result = placeholder_chain.invoke({"context": "What is LangChain?"}) print(result) print(type(placeholder_chain.steps[-2])) # Should print <class 'langchain_core.runnables.passthrough.RunnablePassthrough'>
```

`RunnablePassthrough` can also be used for assignment:

```python
wrap_summary_lambda = RunnableLambda(lambda summary: {"summary": summary}) assign_passthrough = RunnablePassthrough.assign(length=lambda x: len(x["summary"])) summarize_chain = summarize_prompt | llm_gpt4 | output_parser | wrap_summary_lambda assign_chain = summarize_chain | assign_passthrough result = assign_chain.invoke({"context": "What is LangChain?"}) print(result) print(type(assign_chain.steps[-1])) # Should print <class 'langchain_core.runnables.passthrough.RunnableAssign'>
```

Finally, here's an example of using `RunnableParallel`:

```python
from langchain_core.runnables import RunnableParallel summarize_chain = summarize_prompt | llm_gpt4 | output_parser parallel_runnable = RunnableParallel( summary=lambda x: x, # Passes the summary as is length=lambda x: len(x) # Calculates the length of the summary ) parallel_chain = summarize_chain | parallel_runnable result = parallel_chain.invoke({"context": "What is LangChain?"}) print(result) print(type(parallel_chain.steps[-1])) # Should print <class 'langchain_core.runnables.parallel.RunnableParallel'>
```

These examples demonstrate how LCEL and the runnable protocol allow for a flexible composition of language processing chains in LangChain.

## 4\. Splitters and Retrievers

LangChain provides powerful tools for working with documents, including retrievers and splitters. Retrievers are used to search and retrieve relevant documents based on a given query, while splitters are used to break large documents into smaller, more manageable chunks.

![[da192232f6a5114dc01ef5339dbb4557_MD5.jpg]]

### Document Splitting

Let's start by loading a YouTube video transcript using the `YoutubeLoader`:

```python
from langchain_community.document_loaders import YoutubeLoader loader = YoutubeLoader.from_youtube_url( "https://www.youtube.com/watch?v=AOEGOhkGtjI", add_video_info=False ) docs = loader.load()
```

This loader returns a list of documents containing the entire transcript of the video.

Next, we can use the `RecursiveCharacterTextSplitter` to split the loaded documents into smaller chunks:

```python
from langchain_text_splitters import RecursiveCharacterTextSplitter text_splitter = RecursiveCharacterTextSplitter( chunk_size=100, chunk_overlap=20, length_function=len, is_separator_regex=False, ) docs_split = text_splitter.split_documents(docs)
```

The `RecursiveCharacterTextSplitter` is a tool that attempts to keep related chunks of text together. It's particularly useful for maintaining context when splitting large documents.

### Setting Up a Vector Store

To store and retrieve the split documents efficiently, we can use a vector store. In this example, we'll use Redis as the vector store. First, we need to set up the Redis connection:

```python
REDIS_URL = "redis://default:your_redis_password@your_redis_host:your_redis_port" REDIS_HOST = "your_redis_host" REDIS_PASSWORD = "your_redis_password" REDIS_PORT = "your_redis_port" import redis r = redis.Redis( host=REDIS_HOST, port=REDIS_PORT, password=REDIS_PASSWORD) r.ping() r.flushdb()
```

Now, we can create a Redis vector store using the `Redis` class from the `langchain_community` package. We'll use Hugging Face embeddings to generate vector representations of the documents:

```python
from langchain.embeddings import HuggingFaceEmbeddings embeddings = HuggingFaceEmbeddings() from langchain_community.vectorstores.redis import Redis rds = Redis.from_documents( docs_split, embeddings, redis_url=REDIS_URL, index_name="youtube", )
```

### Creating a Retriever

With the vector store set up, we can create a retriever that searches for relevant documents based on a given query:

```python
retriever = rds.as_retriever(search_type="similarity", search_kwargs={"k": 10})
```

This retriever uses similarity search to find the most relevant documents. The `k` parameter specifies the number of documents to return.

We can now use the retriever to find relevant information:

```python
results = retriever.invoke("data analysis")
```

This will return the top 10 most relevant document chunks related to "data analysis" from our stored YouTube transcript.

By using splitters and retrievers, you can efficiently process large amounts of text data and quickly retrieve relevant information for your LLM applications. This forms the foundation for more advanced techniques like Retrieval-Augmented Generation (RAG), which we'll explore in the next section.

## 5\. Building a RAG Chain

Retrieval Augmented Generation (RAG) is a powerful technique that combines document retrieval with language model generation to provide more accurate and contextually relevant responses. RAG enhances the capabilities of LLMs by augmenting their knowledge with external data.

A RAG application is typically built in two main steps:

1.  Indexing the external data (which we did in the previous section)
2.  Retrieving relevant information and generating output with the LLM

![[3f042ad519ca8519097a70b10756df4b_MD5.jpg]]

A RAG App is Build in Two Steps

In the first step, we take documents, chunk them into smaller pieces, convert them into numeric vectors, and load them into a vector database like Redis. This process allows for efficient storage and retrieval of information.

The second step involves using the user's query to fetch relevant context from the vector store. This context, along with the original query, is then sent to the LLM, enabling it to generate a contextually informed output.

Let's build a RAG chain using the Redis-based retriever we set up earlier:

```python
from langchain.prompts import ChatPromptTemplate from langchain_core.output_parsers import StrOutputParser template = """Answer the question based only on the following context: {context} Question: {question} """ prompt = ChatPromptTemplate.from_template(template) output_parser = StrOutputParser() chain = ( {"context": (lambda x: x["question"]) | retriever, "question": (lambda x: x["question"])} | prompt | llm_gpt4 | StrOutputParser() )
```

In this example, we're using a chat prompt template that injects both the context and the user's question into the template. We're also using a string output parser to extract the text output from the LLM.

The chain is set up using LangChain's Expression Language (LCEL). Here's what each part does:

1.  The first line extracts the question from the input data using a lambda function and passes it to the retriever to get the context.
2.  The second line passes the original question directly.
3.  We then use the pipe operator (`|`) to assemble the entire chain, consisting of the input dictionary, the prompt, the LLM (GPT-4), and the string output parser.

Now we can invoke the RAG chain with a question:

```python
answer = chain.invoke({"question": "What can you do with LLama 3?"}) print(answer)
```

This will generate an answer based on the context provided by the documents fetched by the retriever, giving a more informed and contextually relevant response about Llama 3's capabilities.

It's worth noting that while some AI platforms are attempting to abstract away the retrieval process (like OpenAI's Assistant API), having control over the retrieval process can be important for optimizing the performance of chatbots and other AI applications. In particular, when considering metrics like precision (quality of retrieved results) and recall (completeness of retrieved results), which are essential for tasks such as conversion rate optimization in LLM-powered customer interactions.

Tools in LangChain are interfaces that agents, chains, or LLMs can use to interact with the world. A good way to think about tools is that just like humans need tools to perform tasks, LLMs need tools as well. For instance, if you want to do a complex calculation that you can't do in your head, you would need a tool like a calculator or computer program. Similarly, for an LLM to perform certain tasks, it will need access to computational resources or additional data.

LangChain provides several built-in tools, including:

-   Python REPL tool
-   Wikipedia tool
-   YouTube tool
-   Zapier tool
-   Gradio tool

And many more. New tools are constantly being developed.

LangChain also has built-in toolkits, which are collections of tools designed to solve specific tasks. Examples include:

-   AirByte toolkit
-   GitHub toolkit
-   GitLab toolkit

The number of available toolkits is steadily increasing.

There are two main ways to use a tool:

1.  Directly run the tool with a query. This typically returns some data, similar to loaders.
2.  Bind the tools to an LLM. This creates an LLM with access to tools that can be used in chains and agents.

Let's look at an example using the YouTube Search Tool:

```python
from langchain_community.tools import YouTubeSearchTool youtube_tool = YouTubeSearchTool() youtube_tool.run("Rabbitmetrics")
```

This will return a list of videos from the Rabbitmetrics YouTube channel.

We can also bind this tool to an LLM:

```python
llm_with_tools = llm_gpt4.bind_tools([youtube_tool]) msg = llm_with_tools.invoke("Rabbitmetrics YT videos") msg.tool_calls
```

This creates an LLM with access to the YouTube search tool. When we invoke it, we get an AI message with search arguments.

We can extract the tool calls and use them in a chain:

```python
chain = llm_with_tools | (lambda x: x.tool_calls[0]["args"]["__arg1"]) | youtube_tool chain.invoke("Find some Rabbitmetrics videos on langchain")
```

This chain allows us to invoke queries about YouTube videos, with some LLM-based reasoning behind the query. This becomes more powerful when building agents that can use multiple tools to accomplish complex tasks.

## 7\. Building an Agent

Agents are programs capable of reasoning and performing tasks by integrating LLMs with tools. In LangChain specifically, an agent is a class that uses an LLM to choose a sequence of actions to take.

The key difference between an agent and a chain is that in a chain, the sequence of actions is hardcoded, whereas an agent uses the LLM to dynamically decide what actions to take and what tools to use. An agent can loop back and use the LLM to decide on using new tools and taking new actions until it determines the task is complete.

![[4fdb8fa7b89eb686390bfbfe5aa8a2ad_MD5.jpg]]

In Chains Actions are Hardcoded. In Agents we let the LLM decide on Actions.

In theory, agents are more flexible and robust than chains. However, since LLMs can hallucinate, the effectiveness depends on the specific use case.

Let's build an agent for our YouTube use case:

```python
from langchain import hub from langchain.agents import AgentExecutor, create_tool_calling_agent prompt = hub.pull("hwchase17/openai-tools-agent") tools = [youtube_tool] agent = create_tool_calling_agent(llm_gpt4, tools, prompt) agent_executor = AgentExecutor(agent=agent, tools=tools, verbose=True)
```

The prompt template includes an "AgentScratchpad" variable where the agent saves its intermediary steps. We pass the LLM, tools, and prompt to create the agent.

Now we can invoke the agent executor:

```python
agent_executor.invoke( { "input": "Find some langchain YT videos" } )
```

This will use the YouTube search tool to find and rank relevant videos.

We can also create custom tools for the agent. Here's an example of a tool that transcribes YouTube videos:

```python
from langchain_core.tools import tool @tool def transcribe_video(video_url:str) -> str: "Extract transcript from YT video" loader = YoutubeLoader.from_youtube_url( video_url, add_video_info=False ) docs = loader.load() return docs tools = [youtube_tool, transcribe_video] agent = create_tool_calling_agent(llm_gpt4, tools, prompt) agent_executor = AgentExecutor(agent=agent, tools=tools, verbose=True) agent_executor.invoke( { "input": "What topics does the rabbitmetrics YT channel cover?" } )
```

This agent can now search for videos and transcribe them to analyze content.

The key difference between chains and agents is the dynamic decision-making capability of agents. While chains follow a predetermined sequence of steps, agents can adapt their actions based on intermediate results, making them more flexible for complex tasks that may require different approaches depending on the input or intermediate findings.

[[LLM]]  [[Python]]  [[AI Agents]]

[[LangChain Tutorial]]   [[LangChain Agents]]
