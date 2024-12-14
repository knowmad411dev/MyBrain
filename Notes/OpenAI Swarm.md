---
tags:
- agents
- openai
video-url: https://www.youtube.com/watch?v=LBih635lzps&list=WL&index=17
---

## **OpenAI SWAM: Lightweight Multi-Agent Orchestration Framework**

This video discusses **SWAM**, a lightweight, multi-agent orchestration framework released by OpenAI. It provides a detailed walkthrough of the framework’s concepts, showing how it simplifies multi-agent systems. Below is a structured summary, including how-to instructions, key concepts, and code examples.

---

### **Overview of SWAM**

- **What is SWAM?** SWAM is a multi-agent orchestration framework designed to run **OpenAI models** efficiently. It's lightweight and customizable, focused on **agent coordination and execution** without unnecessary abstractions.
- **Closest Comparison:** SWAM’s design resembles **Transformer Agents 2.0** from Hugging Face but aims for a cleaner implementation.
- **Open-Source Nature:**
    - Licensed under **MIT**.
    - Not an official OpenAI product.
    - OpenAI does not actively review issues or pull requests for SWAM.

---

### **Core Concepts**

1. **Agents as Routines**:

    - Agents are encapsulated **LLMs with system prompts**.
    - Each agent has **a set of functions** it can call to handle user input.

2. **Handoff Mechanism**:

    - Agents can **transfer control** to another agent using a function call.
    - This ensures smooth task handoffs in multi-agent setups.

3. **State Machine Design**:

    - SWAM’s architecture functions as a **state machine with conditionals**.
    - Developers have **full control** over state transitions, ensuring easy customization.

---

### **SWAM Usage & Setup Instructions**

**Installation:** To begin, install SWAM via `pip` (or directly clone the repository).

```
pip install swam
```

**Defining Agents:** Each agent has a **name, a system prompt, and functions it can call**.

```python
from swam import Agent

# Define Agent A with a transfer function to Agent B
agent_a = Agent(
    name="Agent A",
    system_instructions="Handle general inquiries.",
    functions=["transfer_to_agent_b"]
)

# Define Agent B with minimal instructions
agent_b = Agent(
    name="Agent B",
    system_instructions="Provide specialized help."
)
```

**Agent Handoff Example:** Agent A can **call a function to transfer control** to Agent B using a function:

```
response = agent_a.run("transfer_to_agent_b", input_data="Help needed!")
print(response)  # This will call Agent B
```

---

### **Detailed Code Example: A Multi-Agent Triaging System**

This example shows **three agents working together**:

1. **Triage Agent**: Directs requests to Sales or Refund agents.
2. **Sales Agent**: Handles product sales queries.
3. **Refund Agent**: Manages refund-related inquiries, offering discounts if needed.

#### Code Snippet

```python
from swam import Agent

# Triage Agent - Redirects to Sales or Refund
triage_agent = Agent(name="Triage Agent")
triage_agent.add_function("transfer_to_sales")
triage_agent.add_function("transfer_to_refund")

# Sales Agent - Enthusiastic about sales
sales_agent = Agent(
    name="Sales Agent",
    system_instructions="Promote products energetically!"
)
sales_agent.add_function("transfer_to_triage")

# Refund Agent - Handles refunds and discounts
refund_agent = Agent(
    name="Refund Agent",
    system_instructions="Assist with refunds. Offer discounts if needed.",
    functions=["process_refund", "apply_discount"]
)
refund_agent.add_function("transfer_to_triage")

# Infinite Loop to Interact with User Input
while True:
    user_input = input("User: ")
    response = triage_agent.run(user_input)
    print(f"Agent Response: {response}")
```

---

### **How SWAM Differs from Other Frameworks**

- **Transparency and Client-Side Control:** SWAM runs similarly to the **chat completion API** but executes locally, allowing developers full transparency and control.
- **No Memory Handling:** SWAM doesn’t include **persistent memory**; developers need to implement memory management themselves.
- **Highly Customizable:** It’s designed as a **state machine**, making it scalable and flexible for **multi-agent coordination**.

---

### **Comparison with OpenAI Assistance API**

- **SWAM**: Developer-focused, client-side, lightweight.
- **OpenAI Assistance API**: Hosted solution with built-in tools but less customizable.

---

### **Key Takeaways**

- **SWAM’s focus** is on **coordination between agents** via handoff, ensuring easy-to-manage transitions.
- Instead of tool usage, **agents are treated like function calls**, allowing the smooth execution of tasks.
- You can **extend SWAM** or build similar frameworks using their **design patterns**.

---

### **References and Resources**

- **GitHub Repository** (with Code and Examples): SWAM on GitHub
- **Detailed Blog Post on SWAM Design**: Orchestrating Agents, Routines, and Handoffs

---

### **Conclusion**

SWAM offers a promising approach for **developers wanting granular control** over multi-agent orchestration. The framework’s **state machine-like design** makes it highly adaptable and suitable for custom workflows. Future updates may bring additional functionalities, but it already serves as a solid foundation for multi-agent systems.

[[OpenAI Swarm Framework]] [[Artificial intelligence]]  [[OpenAI]]  [[Python]]