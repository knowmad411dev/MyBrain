---
tags:
- agents
video-url: https://www.youtube.com/watch?v=MkqkiJgnDxk&list=WL&index=3
---
## **PydanticAI - Building a Research Agent

### Overview of the Research Agent Tutorial

The presenter aims to create a research agent using Pydantic AI, similar in concept to platforms like Perplexity. They employ asynchronous searching through Tavily and Duck Duck Go, combined with Pydantic to generate structured responses. The implementation is done in a Jupyter Notebook for accessibility and interactive use.

**Key Concepts Covered**:
1. Setting up search engines (Duck Duck Go and Tavily).
2. Asynchronous searches using Python packages.
3. Creating a research agent using Pydantic AI to perform multiple searches.
4. Structuring the output for easy use and customizability.

### Code Examples and Instructions

#### 1. Search Engines Setup

The code sets up two search engines:

- **Duck Duck Go**: Uses an unofficial Python package that supports both synchronous and asynchronous calls.
- **Tavily**: A paid API offering 1,000 free monthly calls, suitable for this application without credit card requirements.

**Example**:
```python
# Install Python libraries required for Duck Duck Go and Tavily searches.
# pip install duckduckgo-search
# pip install tavily
```
**Important Note**: Duck Duck Go is limited due to rate limiting; Tavily provides more consistent availability.

#### 2. Dependency and Data Class Setup

To structure the data flow, multiple dependencies are defined:

- **Search Data Class**: Manages how many results are returned for a given query.
- **Result Type**: Specifies how the response is structured, consisting of a title, a main content section, and bullet points for the summary.

**Example**:
```python
from pydantic import BaseModel
from dataclasses import dataclass

@dataclass
class SearchData:
    max_results: int  # Define the maximum number of search results per query.

class ResultType(BaseModel):
    research_title: str
    research_main: str
    research_bullets: str
```

#### 3. Building the Agent with OpenAI Models

The presenter used OpenAI's GPT-4 model (possibly referring to a specific variation like GPT-4o). The flexibility to switch models like "GPT-4o-mini" or "Gemini" is highlighted.

**System Prompt Example**:
The agent is configured to search using keywords to determine how many searches to do and how to combine those results.
```python
system_prompt = """
You are a helpful research assistant. You are an expert in research.
You are given a question, you generate 3-5 searches using strong keywords.
Each search will have a query number, and you must combine the results into a coherent response.
"""
```

The idea is to allow the assistant to be modified easily, e.g., adapting it to focus on academic or commercial research by changing the system prompt.

#### 4. Search Agent Tool Setup

The presenter defines a tool for executing search queries, which could use either Duck Duck Go or Tavily. The `@search_agent.tool` decorator is used to simplify setting up multiple search tools.

**Example Code**:
```python
from some_module import search_agent  # Placeholder for where this module comes from.

@search_agent.tool
async def search_tool(query: str, max_results: int) -> dict:
    # Assuming Tavily search
    response = await tavily_search(query, max_results)
    return response
```
- **Query and Query Number**: Managed by the LLM to keep track of searches and their results.
- **Dependencies**: Defined with flexibility for user inputs.

#### 5. Injecting System Dependencies

The presenter demonstrates injecting dependencies dynamically—e.g., today's date into the system prompt.

**Example Code**:
```python
from datetime import datetime

date_string = datetime.now().strftime("%Y-%m-%d")
system_prompt_with_date = system_prompt + f"\nIf you need today's date, it is {date_string}."
```

The user can dynamically inject dates or other information into the system prompt to adapt the model's responses to a specific context.

#### 6. Example Agent Execution

An example query is demonstrated, requesting a detailed biography of Sam Altman. The agent:

- Executes 3 to 5 searches asynchronously.
- Combines the results using the structure defined in `ResultType`.

**Example**:
```python
query = "Give me a very detailed bio on Sam Altman"
result = await research_agent.execute(query)

# Structured Output
print(result.research_title)
print(result.research_main)
print(result.research_bullets)
```

The search agent can dynamically decide how many searches to execute based on the user query’s level of detail.

#### 7. Handling Date Information for Current Events

When a query involves the latest news (e.g., "What is the latest new AI news?"), the model uses the current date. By adding a date injection mechanism, the assistant can provide up-to-date answers.

**Modified System Prompt with Date**:
```python
system_prompt_with_date = """
You are a helpful research assistant. You are an expert in research.
If you need today's date, it is 2024-12-05.
"""
```

This updated prompt enables the model to perform current news searches without defaulting to outdated content.

#### 8. Customizing Response Structure

The response structure can be customized using the `ResultType` class. For example, if the user needs a more detailed answer (e.g., a 500-word essay), the schema could be modified to add different sections or constraints.

**Example Modifying ResultType**:
```python
class ResultType(BaseModel):
    research_title: str
    research_intro: str
    research_main: str
    research_bullets: list[str]
```

The flexibility of the result format allows different structures based on specific needs, and these changes are reflected in the overall workflow.

### GitHub Links and References

The presenter does not explicitly mention any GitHub links, but here are the typical places where this project’s components could be hosted:

1. **Search Tools Integration**:
   - **Duck Duck Go Python Package**: [GitHub Repository](https://github.com/deedy5/duckduckgo-python)
   - **Tavily Python Library**: Likely available through the Tavily API documentation.

2. **Research Agent Project**:
   - The Jupyter Notebook, agent setup, and code examples are ideal for GitHub. The presenter might host these scripts under a general AI projects repository.

3. **Pydantic Documentation and GitHub**:
   - Pydantic GitHub: [Pydantic GitHub Repository](https://github.com/pydantic/pydantic)

### How-To Instructions Summary

1. **Install Dependencies**:
   - Use `pip install` to install Pydantic, Tavily, and Duck Duck Go libraries.
2. **Setup Dependencies**:
   - Create data classes for managing search queries and responses.
3. **Build the Agent**:
   - Configure an OpenAI-based LLM for conducting searches.
   - Use a system prompt to define the search process.
4. **Run Search Queries**:
   - Execute the agent using an async model to return structured data.
5. **Customize Responses**:
   - Modify the output schema (`ResultType`) as per specific requirements.
6. **Inject Dynamic Data**:
   - Use datetime to add up-to-date information to the system prompt.

This video is ideal for understanding how to build a research agent using Pydantic AI and integrate multiple search engines with an LLM, providing a reusable template for research tasks. If you want a working implementation, it would be advisable to look for a GitHub repository containing these examples or recreate them based on the explanations provided here.

[[AI Agents]]  [[Python]]  [[Pydantic AI]]