---
github_link: https://github.com/pydantic/pydantic-ai
tags:
- agents
- python
video-url: https://www.youtube.com/watch?v=hoIy26Rlk5s&list=WL&index=2
---
# Overview of Pydantic AI

Pydantic AI is an agent framework developed by the creators of Pydantic, a popular Python library known for its data validation features. Pydantic AI aims to make the development of production-grade applications with generative AI less painful, offering type-safe integration and leveraging familiar Python development practices. In this overview, we will explore Pydantic AI, including its key features, usage examples, how to get started, and where to find it on GitHub.

### Key Features

1. **Built by Pydantic's Team**: Pydantic AI inherits all the validation strengths of the Pydantic library, which is well-respected in the Python community, and integrates with OpenAI, Gemini, and Anthropics.
2. **Model Agnostic**: Pydantic AI currently supports OpenAI, Gemini, and Gro models, with support for Anthropic models coming soon.
3. **Streaming and Structured Responses**: It can validate streamed responses from LLMs, allowing for token-by-token response validation—ideal for conversational AI.
4. **Novel Dependency Injection System**: This system enables effective testing and iterative development, ensuring that LLM interactions are easily managed and integrated.
5. **Integration with LogFire**: Pydantic AI integrates with LogFire for observability, debugging, and monitoring your LLM applications.

### Why Use Pydantic AI?

Pydantic AI offers a production-grade agent framework that brings together various powerful features, making it suitable for building scalable applications. Unlike other agentic frameworks, Pydantic AI places significant emphasis on type safety, data validation, and model-agnostic development, all while integrating seamlessly with existing Python applications.

### Getting Started

To begin using Pydantic AI, you need to install the Pydantic AI package and familiarize yourself with its core components such as agents, dependencies, and structured result types. Below, we will demonstrate two use cases to illustrate the functionality of Pydantic AI.

#### Example 1: A Basic Agent with Pydantic AI

The following simple example illustrates how to use Pydantic AI to set up an agent with a static system prompt.

```python
# Import the necessary components from Pydantic AI
from pydantic_ai import Agent

# Define the LLM and system prompt
llm = "Gemini 1.5"  # The LLM to be used

# Create an agent instance
agent = Agent(
    llm=llm,
    system_prompt="You are an AI assistant. Please answer any questions presented."
)

# Use the agent to respond to a query
response = agent("What is the capital of France?")
print(response)
```

This code snippet shows how to initialize an agent with a specific LLM (in this case, Gemini 1.5) and use a static system prompt to respond to a user query.

#### Example 2: Customer Support Agent for a Bank

This more advanced example demonstrates how to create a customer support agent using Pydantic AI. This agent dynamically retrieves customer information and provides specific support functions, such as checking account balances or blocking cards.

```python
# Import necessary libraries and components
from dataclasses import dataclass
from pydantic import BaseModel, Field
from pydantic_ai import Agent, RunContext

# Fake database for customer information
@dataclass
class FakeCustomerDatabase:
    customer_data = {
        "john_doe": {"balance": 1234.56, "blocked": False},
    }

# Define dependencies for the support agent
@dataclass
class SupportDependencies:
    db: FakeCustomerDatabase

# Define a structured result type for the agent's output
class SupportResult(BaseModel):
    support_advice: str
    block_card: bool = Field(False)
    risk_level: str

# Create the support agent
support_agent = Agent(
    llm="GPT-4.0",
    system_prompt="You are a customer support agent for a bank. Assist the customer and assess risk levels.",
    result_type=SupportResult,
    dependencies=SupportDependencies(FakeCustomerDatabase())
)

# Function to handle balance inquiries
def get_customer_balance(customer_id: str):
    customer_info = FakeCustomerDatabase.customer_data.get(customer_id)
    if customer_info:
        return customer_info["balance"]
    else:
        return "Customer not found."

# Example interaction
customer_id = "john_doe"
response = support_agent(f"What is my balance? Customer ID: {customer_id}")
print(response)
```

In this example:

1. **Dependencies** are defined to provide access to customer data.
2. **SupportResult** is used to structure the responses from the agent.
3. **Agent Initialization**: The agent is set up with GPT-4.0, and customer support functionalities like checking the balance are provided using the defined dependencies.

### GitHub Repository

You can find the source code, examples, and complete documentation for Pydantic AI on GitHub at the following link:

[Pydantic AI GitHub Repository](https://github.com/pydantic/pydantic-ai)

### Conclusion

Pydantic AI is a powerful addition to the growing list of agent frameworks. By leveraging Pydantic's well-known validation features and integrating LLM capabilities, it provides a model-agnostic, production-grade solution for building generative AI applications. With features like type-safe validation, dependency injection, and the ability to seamlessly stream and structure responses, it is well-positioned for teams looking to build scalable, reliable AI-driven systems.

### Next Steps

- **Explore the Documentation**: Dive deeper into the [GitHub documentation](https://github.com/pydantic/pydantic-ai) to understand the full breadth of features.
- **Experiment with Agents**: Try building custom agents to fit your use case, leveraging dynamic prompts and structured responses.
- **Integrate LogFire**: Set up observability using LogFire for monitoring and debugging purposes.

Happy coding with Pydantic AI!

[[Python]]  [[AI Agents]]