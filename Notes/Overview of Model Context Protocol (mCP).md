---
tags:
- editors
video-url: https://www.youtube.com/watch?v=u6444EjemKo&list=WL&index=1
---
## **Overview of Model Context Protocol (mCP)

The text you've provided describes a detailed walk-through of setting up and utilizing the **Model Context Protocol (mCP)**, a newly launched open-source standard by Anthropic for connecting generative AI models to external tools. Here’s a comprehensive overview including key instructions and code examples mentioned.

### **Overview of Model Context Protocol (mCP)**

The **Model Context Protocol (mCP)** is a standardized way for generative models (clients) to interact with tools. It allows separation between the tool maker and the client maker, both of which can independently operate while still integrating efficiently. The protocol is designed to work across different language models, and it is completely open source.

#### **Purpose of mCP:**

1. **Standardization**: Provides a standardized way to link tools and clients, replacing the older method of hard-coding tool definitions into application code.
2. **Open Source Flexibility**: Works with any model, allowing flexibility in using tools from different models or platforms.
3. **Separation of Concerns**: Tool definitions live in the mCP server, not within individual clients.

### **Architecture of mCP**

The architecture is composed of:

- **Client** (such as Claude Desktop or a custom client)
- **mCP Server** (which hosts tool definitions)
- **Resources** (like a SQLite database)

The **mCP Server** acts as an intermediary that provides access to the tools. For instance, in the given example, Claude Desktop is used to interact with a SQLite database through the mCP server. The mCP server holds the definitions of the tools that the client uses.

### **How mCP Works in Practice**

The walk-through shows how to create a custom client using different large language models to connect to tools via mCP.

#### **Key Concepts and Tools:**

1. **mCP Server**: Hosts tool definitions; the client connects to the server to determine which tools are available.
2. **SQLite Database**: The example uses a SQLite database to demonstrate interactions via mCP.
3. **Python Package**: Uses a Python package manager called **uvicorn** to run the server and client interactions.
4. **Bedrock Converse API**: The walkthrough uses **Amazon Bedrock Converse API** to interact with different large language models (e.g., Claude, Mistral, Meta’s Llama).

### **How-To Instructions**

1. **Setup the Environment:**
   - The **quick start guide** linked in the original article helps you set up the mCP environment.
   - **SQLite Database**: Set up a simple SQLite database on your local system to connect through the mCP server. This involves deploying a sample SQLite database and adding some example data.
   - The mCP uses **standard input/output** to communicate rather than a network connection, leveraging **uvicorn** as the package manager.

2. **mCP Quick Start Guide:**
   - The guide will help you deploy the database and configure the client (such as Claude Desktop).
   - Follow the instructions to add a configuration snippet to the **Claude Desktop** setup to connect with the mCP server.

3. **Python Project Configuration:**
   - Use **uvicorn** to run the server. You pass in the package name and some options to set up the server.
   - Set up a **configuration file** for the client to specify the mCP server location.

### **Creating Your Own Application**

The tutorial shows how to create a custom client application using **mCP** and connect it to different models via Amazon Bedrock Converse API.

#### **Project Files Overview:**

- **app.py**: The main script for the application.
- **converse_agent.py**: Uses the Amazon Bedrock Converse API, wraps tools, and response processing.
- **converse_tools.py**: Manages tools used by the Converse agent.

#### **Workflow and Code Highlights**

1. **Define the Model**:
   ```python
   model_id = "Claude 3.5 Sonet Version 2"
   # Other available models include Meta's Llama, Mistral, etc.
   ```

   You start by defining the **model ID** you want to use, which can be switched easily in the code.

2. **Agent and Tool Manager Setup**:
   ```python
   converse_agent = ConverseAgent(model_id)
   tool_manager = ConverseToolManager()
   ```

   Set up the agent and tool manager to handle undifferentiated heavy lifting.

3. **System Prompt**:
   ```python
   system_prompt = "You are a helpful assistant that can use tools to answer questions and perform tasks."
   ```

   Set up a simple system prompt for the agent.

4. **mCP Client Configuration**:
   ```python
   mcp_client = MCPClient(server_parameters)
   ```

   The **mCP client** is created by passing in server parameters. The client then communicates with the mCP server to get the available tools.

5. **Tool Registration**:
   ```python
   available_tools = mcp_client.get_available_tools()
   for tool in available_tools:
       agent.register_tool(tool.name, tool.description)
   ```

   Tools are registered with the agent using information retrieved from the mCP server.

6. **Chatbot Loop**:
   The script enters a **command-line chatbot** loop where you can enter prompts, and the agent will invoke tools as needed.
   ```python
   while True:
       user_input = input("Enter your prompt: ")
       response = agent.invoke(user_input)
       print(response)
   ```

### **Running the Application with Different Models**

- The application can be connected to different models by simply changing the model ID.
- Examples:
  - **Mistral Model**: Create tables in the SQLite database.
    ```python
    model_id = "Mistral Large 2"
    ```
  - **Meta's Llama Model**: Perform queries on the database.
    ```python
    model_id = "Meta's Llama 3.2"
    ```

### **Demonstration of Tool Usage in Code**

- The agent can answer questions like:
  ```python
  # Example question to the chatbot
  prompt = "How many products are in the products table?"
  ```
- The agent uses the tools from the server to run SQL queries, dynamically invoking tools based on the question.

### **Handling Compatibility Issues**

- During implementation, a compatibility issue was discovered with tool names containing hyphens. The solution was to sanitize tool names by replacing hyphens with underscores.

  ```python
  def sanitize_tool_name(name):
      return name.replace('-', '_')
  ```

### **Example Output**

- **Product Count**:
  - Input: `"How many products are in the products table?"`
  - Output: `"There are 20 products in the product table."`
- **Weather Table Creation**:
  - Input: `"Create a weather table with sample observations."`
  - Output: `"Table created and Sample weather observations inserted successfully."`

### **Issues Encountered and Workarounds**

- **Insights Tool Problem**:
  - A particular **Insights Tool** failed to work in the mCP setup, which involved updating a memo resource with data insights.
  - The memo is a resource, not a tool, and attempts to append insights failed without completion. This issue is highlighted as an area that needs further debugging and contributions.

### **Summary**

The text details a practical implementation of the **Model Context Protocol (mCP)** to connect a client application to external tools using different language models. Key points include:

- Using the **mCP server** to register tools, keeping tool definitions separate from the client.
- The flexibility provided by **Bedrock Converse API** to switch between multiple models such as Claude, Mistral, or Meta's Llama.
- A step-by-step guide to setting up SQLite as the back-end resource and interacting with it through an **agentic workflow**.

The **Python code examples** demonstrate:

- Setting up an mCP server and client.
- Creating an agent that can invoke tools as per user input.
- Handling issues like tool name compatibility and debugging unsuccessful interactions.

### **Key Takeaways**

- **mCP** is a powerful tool for decoupling client-tool interaction in a standardized, open-source manner.
- The architecture allows switching between different **large language models** seamlessly by changing the model ID.
- **Agentic Workflow** is used to perform tasks by invoking tools dynamically as required.

If you have any more questions or need deeper insights into any specific part of this process, feel free to ask!

[[Claude Agents]] [[Code Editor]]