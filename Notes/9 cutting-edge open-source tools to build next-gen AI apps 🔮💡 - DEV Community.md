---
tags:
- editors
---
## **9 cutting-edge open-source tools to build next-gen AI apps

I have been building and working with AI applications for over years. While building any AI application, I use multiple third-party tools and libraries to simplify the whole development process.

In this blog, I have curated 9 super-handy but lesser-known tools that I use to ease out the work.

Feel free to explore and try out these tools for your projects.

---

### 1. [Composio](https://dub.composio.dev/nPvXxAP)👑- AI integrations and tooling platform

Imagine having the power to build your own AI agents and seamlessly integrate them into tools like Discord, Trello, Jira, or Slack. That’s what Composio is!

It's an open-source platform that makes adding AI functionality to your applications easy and accessible. Whether you're customizing  [[AI agents]] or plugging it into your favorite tools, Composio has you covered.

#### Some use cases of Composio:

- Build Coding agents to optimize the code present in the Github repository.
- Build AI bots for your Slack channels and Discord servers that can autonomously interact with the users and respond to their queries.
- AI agent to provide a summary of reports or documents.

**Install Composio**:

```bash
pip install composio-core
```

**Add a [[GitHub]] integration**:

Composio manages user authentication and authorization for you.

Here’s an example to automatically star a GitHub repository using Composio’s GitHub integration:

```python
from openai import OpenAI
from composio_openai import ComposioToolSet, App

openai_client = OpenAI(api_key=OPENAI_API_KEY)

# Initialise the Composio Tool Set
composio_toolset = ComposioToolSet(api_key=COMPOSIO_API_KEY)

# Get GitHub tools that are pre-configured
actions = composio_toolset.get_actions(actions=[Action.GITHUB_ACTIVITY_STAR_REPO_FOR_AUTHENTICATED_USER])

my_task = "Star a repo ComposioHQ/composio on GitHub"

# Create a chat completion request to decide on the action
response = openai_client.chat.completions.create(
    model="gpt-4-turbo",
    tools=actions,  # Passing actions we fetched earlier.
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": my_task}
    ]
)
```

Use this [[Python]] code to create an AI agent that automatically stars a GitHub repository.

Check out the Composio [docs](https://docs.composio.dev/introduction/intro/overview) to learn more. Explore more advanced [examples](https://github.com/ComposioHQ/composio/tree/master/python/examples) built using Composio.

[Star the Composio Repo ⭐](https://dub.composio.dev/FZLK76b)

---

### 2. [Letta](https://www.letta.com/) - Build stateful [[LLM]] Applications

Letta is your go-to platform for building smart, stateful applications powered by large language models (LLMs). It's like giving AI systems memory so they can deliver long-term, personalized, and context-aware results.

**Get started with Letta**:

Install the Letta library:

```bash
pip install letta
```

**Send a message to an agent**:

```python
from letta import create_client

# connect to the server
client = create_client(base_url="http://localhost:8283")

# send a message to the agent
response = client.send_message(
    agent_id="agent-09950586-6313-421c-bf7e-2bba03c30826",
    role="user",
    message="hey!! how are you?"
)
```

Check out the Letta [docs](https://docs.letta.com/introduction) to learn more.

[Star the Letta Repo ⭐](https://github.com/letta-ai/letta)

---

### 3. [Rasa](https://rasa.com/) - Build Conversational AI Experiences

Rasa is an open-source platform that makes building advanced conversational AI applications a breeze. With Rasa, you can create intelligent chatbots and virtual assistants that truly understand natural language.

**Add your API keys**:

```bash
RASA_PRO_LICENSE='your_rasa_pro_license_key_here'
OPENAI_API_KEY='your_openai_api_key_here'
```

Activate your Python environment:

```bash
source .venv/bin/activate
```

Check out the Rasa [docs](https://rasa.com/docs/) to learn more.

[Star the Rasa Repo ⭐](https://github.com/RasaHQ/)

---

[[Free AI Tools]]  [[GPT]]
