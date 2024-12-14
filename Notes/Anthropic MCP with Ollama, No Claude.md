---
github_link: https://github.com/chrishayuk/mcp-cli
tags:
- ollama
- editors
video-url: https://www.youtube.com/watch?v=9mciRwpcLNY&list=WL&index=2
---
## **Anthropic MCP with Ollama, No Claude

### **Overview of the Model Context Protocol (MCP)**

The text introduces **Model Context Protocol (MCP)**, a framework designed to connect **Large Language Models (LLMs)** to external data sources and tools. This guide explains how to:

1. Use MCP in a custom **Command Line Interface (CLI)** with various LLMs, such as **OpenAI** and **Llama**.
2. Integrate MCP for enabling dynamic interactions between LLMs and external resources, such as **SQLite** databases.
3. Build your own MCP application using **JSON-RPC** as a communication protocol.

---

### **Key Features of MCP**

- **Host-Client Architecture**:
  - **Host**: The core MCP application, such as a CLI.
  - **Client**: Database or resource tools that connect to the host.
  - **Server**: Backend MCP server, like an **SQLite** server, to which the host connects.
- **Compatibility**:
  - MCP supports **OpenAI**, **Llama**, and other models that are capable of function calling.
- **Protocol Communication**:
  - MCP utilizes **JSON-RPC 2.0** for efficient communication, enabling seamless tool usage by LLMs.

---

### **How-To Guide for Implementing MCP**

#### **1. Setting Up MCP**

##### **Architecture Overview**

- **Host**: The MCP app (e.g., CLI) manages communication.
- **Server**: Resource provider, such as a SQLite server.
- **Clients**: Resources like databases or other tools.

##### **Step-by-Step Setup**

1. **Prepare the Environment**:
   - Install necessary Python libraries.
   - Set up an `.env` file to include API keys:
     ```plaintext
     OPENAI_API_KEY=<your_openai_api_key>
     ```

2. **Run MCP Server**:
   - Start the SQLite MCP server using the following command:
     ```bash
     uvx mcp_server_sqlite --db-path test.db
     ```

3. **Test Server Connection**:
   - Use the following Python function to ping the server and ensure it's active:
     ```python
     async def ping_server():
         response = await client.send_message({
             "jsonrpc": "2.0",
             "id": "ping-1",
             "method": "ping"
         })
         print(response)
     ```

---

#### **2. Implementing MCP in a Custom CLI**

##### **Basic Workflow**

- **CLI Commands**:
  - `ping`: Checks server availability.
  - `list_tables`: Retrieves available database tables.
  - `describe_table`: Shows the table schema.
  - `execute_query`: Runs SQL commands like `SELECT`.

##### **Example: CLI Code Implementation**

```python
async with StandardIOClient(server_params) as client:
    # Initialize the server
    await client.send_initialize_message()
    
    # Fetch available tables
    response = await client.send_message({
        "jsonrpc": "2.0",
        "id": "list_tables",
        "method": "tools.call",
        "params": {"name": "list_tables"}
    })
    print(f"Available tables: {response}")
```

##### **Switching Between Models**

- Set your desired provider directly within the CLI configuration:
   ```python
   provider = "openai"  # Or "ollama"
   model = "llama-3.2"  # Or "gpt-40-mini"
   ```

---

#### **3. Understanding the MCP Protocol**

MCP relies on **JSON-RPC 2.0** for message-based communication between the host and server. Key interactions include initialization and pinging the server.

##### **Initialization**

- The host sends an **initialize** message to initiate the connection:
  ```json
  {
      "jsonrpc": "2.0",
      "id": 1,
      "method": "initialize",
      "params": {
          "protocol_version": "1.0",
          "capabilities": ["list", "query"],
          "client_info": {"name": "cli-app", "version": "1.0"}
      }
  }
  ```
- The server responds, detailing its supported capabilities.

##### **Ping Message**

- Use a **ping** message to check server status:
  ```json
  {
      "jsonrpc": "2.0",
      "id": "ping-1",
      "method": "ping"
  }
  ```

---

#### **4. Integrating Tools into MCP**

Tools are defined using **JSON schema**, enabling easy integration and use with MCP.

##### **Defining Tools**

- Each tool is defined with its **name**, **description**, and **input schema**:
  ```json
  {
      "name": "list_tables",
      "description": "Retrieve all tables in the database",
      "input_schema": {
          "type": "object",
          "properties": {}
      }
  }
  ```

##### **Using Tools in Chat Mode**

1. **Generate System Prompt**: Prepare a system prompt to describe tool capabilities:
   ```plaintext
   In this environment, you can use tools to interact with the database:
   - list_tables: List available tables.
   - describe_table: Retrieve table schema.
   - execute_query: Run SQL queries.
   ```
2. **Integrate into LLM**: Pass the system prompt into the LLM's context for enhanced tool calling capabilities.

---

#### **5. Function Calling in MCP**

Function calling allows LLMs to use the tools dynamically during interaction.

##### **Workflow**

1. **Fetch Tools**: Retrieve the tools available from the server.
2. **Generate Prompt**: Add tool descriptions to the system prompt for the LLM.
3. **Tool Execution**: Pass tool calls from the LLM to the server for execution.

##### **Tool Call Example**

```python
# Call a tool (list_tables)
response = await client.send_message({
    "jsonrpc": "2.0",
    "id": "tool-1",
    "method": "tools.call",
    "params": {
        "name": "list_tables",
        "args": {}
    }
})
print(f"Tool Response: {response}")
```

---

### **Simplified Example: Minimal MCP Implementation**

If you want a quick and minimal setup, you can create a simplified script (`test.py`):

```python
# Minimal MCP Implementation
async def main():
    config = load_config("server_config.json")
    async with StandardIOClient(config) as client:
        # Initialize server
        await client.send_initialize_message()
        # Ping server
        response = await client.send_ping()
        print(f"Server Response: {response}")

if __name__ == "__main__":
    import asyncio
    asyncio.run(main())
```

---

### **Summary**

1. **Set Up Server**: Start the MCP-compatible server (e.g., SQLite).
2. **Protocol Implementation**: Use **JSON-RPC 2.0** for communication.
3. **CLI Setup**: Build your CLI for interaction with the server.
4. **Enable Tool Integration**: Use JSON schema to define tools for function calls.
5. **Test & Extend**: Interact with MCP, add more commands, and iterate.

By following these steps, you can implement a custom MCP system to connect LLMs with diverse tools and resources. Use these examples as starting points for your implementation to build and extend your own capabilities.

[[Claude Agents]]  [[Ollama]]  [[Python]]  [[LLM]]  [[Code Editor]]  