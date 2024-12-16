---
tags:
- openai
- python
video-url: https://www.youtube.com/watch?v=q7_5eCmu0MY
---

## **Overview of OpenAI Swarm**

OpenAI Swarm is an open-source AI agent orchestration tool that allows you to write clean and simple Python code to build AI agents and seamlessly connect them to accomplish complex tasks. It aims to provide an educational and experimental approach to AI agent orchestration by showcasing best practices in how agents can be coordinated effectively. While Swarm is not production-grade software, it is an excellent tool for learning how to build robust agent architectures.

Swarm is especially useful for managing multiple AI agents that need to collaborate on complex tasks. For instance, instead of overwhelming a single large language model (LLM) with extensive instructions, Swarm facilitates breaking the task into smaller specialized components, with multiple agents handling distinct parts of the overall job. This modular approach helps avoid the "needle in a haystack" problem that occurs when one LLM is overloaded with too many instructions, reducing efficiency and accuracy.

The library includes well-documented examples, making it ideal for those wanting to learn how to build an orchestrated system of multiple agents. In this guide, we will walk through building a simple AI swarm to manage a SQL database, involving AI agents that specialize in querying, managing tables, and cleaning data.

---

**How to Set Up and Use OpenAI Swarm**

### Step 1: Installation and Requirements

First, start by cloning the Swarm repository from GitHub. You can find the repository by searching for "OpenAI Swarm GitHub." After cloning, follow the instructions to install it:

1. Clone the repository:
   ```bash
   git clone https://github.com/openai/swarm.git
   cd swarm
   ```

2. Install required Python packages by running:
   ```bash
   pip install -r requirements.txt
   ```

3. Set up your OpenAI API key by creating an environment variable:
   ```bash
   export OPENAI_API_KEY="your_openai_api_key_here"
   ```

Make sure you have SQLite installed since we will be using it for the database.

### Step 2: Set Up Your Database

For the purpose of this tutorial, we will create a SQLite database to store RSS feed data. We will also add some mock data using a simple Python script:

1. Create SQL tables and mock data:

   ```sql
   CREATE TABLE rss_sources (
       id INTEGER PRIMARY KEY,
       name TEXT,
       url TEXT
   );

   CREATE TABLE articles (
       id INTEGER PRIMARY KEY,
       source_id INTEGER,
       title TEXT,
       content TEXT,
       published_date DATE,
       FOREIGN KEY (source_id) REFERENCES rss_sources(id)
   );
   ```

2. Insert mock data into the tables to play around with.

### Step 3: Writing Python Code for Swarm

Below is the Python code to create and orchestrate a swarm of AI agents using OpenAI Swarm to manage our SQL database.

**Step 3.1: Import Required Packages**

```python
import sqlite3
import swarm

# Establish a connection to the SQLite database
conn = sqlite3.connect('rss_feed.db')
```

**Step 3.2: Define a SQL Tool for Agents**

This is a helper tool for agents to execute SQL queries.

```python
def run_sql_query(sql):
    cursor = conn.cursor()
    cursor.execute(sql)
    records = cursor.fetchall()
    if not records:
        return "No records found."
    return records
```

**Step 3.3: Create Agent Instructions**

Define instruction strings for our router agent and specific query agents:

```python
def router_instructions():
    return "You are an orchestrator. Route user queries to the correct agent based on the request."

def feed_agent_instructions():
    return "You are an RSS feed expert. Handle queries related to RSS feed data."

def analytics_agent_instructions():
    return "You are an analytics expert. Handle questions related to data insights and analysis."
```

**Step 3.4: Create Agents**

We define three agents: a router agent, an RSS feed agent, and an analytics agent.

```python
router_agent = swarm.Agent(name="router", instructions=router_instructions())

rss_feed_agent = swarm.Agent(name="rss_feed", instructions=feed_agent_instructions(), functions=[run_sql_query])

analytics_agent = swarm.Agent(name="analytics", instructions=analytics_agent_instructions(), functions=[run_sql_query])
```

**Step 3.5: Setting Up Transfers Between Agents**

We need to create transfer functions so that the router can send tasks to specialized agents and the specialized agents can hand results back.

```python
def route_to_feed(query):
    return rss_feed_agent.run(query)

def route_to_analytics(query):
    return analytics_agent.run(query)

# Assign routing functions to the router agent
router_agent.add_route("rss_feed", route_to_feed)
router_agent.add_route("analytics", route_to_analytics)
```

**Step 3.6: Running the Agent Swarm**

Lastly, we create a demo loop that allows us to interact with the agents.

```python
def run_demo():
    while True:
        user_query = input("Ask a question: ")
        response = router_agent.run(user_query)
        print(response)

# Start the interactive demo
run_demo()
```

### Step 4: Running the Program

To run the program, save the Python script (let's call it `swarm_demo.py`), and execute it from your terminal:

```bash
python swarm_demo.py
```

You can now ask questions like "How many RSS feeds do we have?" or "What is the most popular category among users?" The router will determine which agent to call based on the question, allowing specialized agents to process the data more efficiently.

### Example Output

- **Question**: "How many users are there in the database?"
  - **Response** (from the user agent): "We currently have 5 users on the platform."
- **Question**: "How many RSS feeds do we have?"
  - **Response** (from the RSS feed agent): "We have a total of 5 fantastic RSS feeds available! Isn't it amazing?"

### Summary

OpenAI Swarm simplifies the process of building complex orchestrations of multiple AI agents working in unison to achieve a task. By breaking down large tasks and distributing them among specialized agents, you can achieve efficiency and avoid overwhelming a single model.

Swarm is not designed for production-grade software but rather as a means of learning the best practices for agent coordination. It is easy to extend this setup to add more agents, different tools, or connect Swarm to more complex databases and APIs.

Give Swarm a try and experiment with creating agent-based workflows that make AI management of complex data seamless and insightful.

[[Python]]  [[OpenAI How-to LLM Models]]