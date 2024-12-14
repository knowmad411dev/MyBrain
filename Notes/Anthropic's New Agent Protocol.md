---
tags:
- agents
- editors
video-url: https://www.youtube.com/watch?v=8mU2OeOCIrE&list=WL&index=2
---
# Overview of Anthropic's Model Context Protocol (MCP)

Anthropic has introduced the **Model Context Protocol (MCP)**, an open standard that aims to improve how large language models (LLMs) interact with external data and systems. This protocol is similar to plugins and search integrations but goes beyond by offering a general, open-source standard that any model or system can use.

### Key Features of MCP

1. **Interoperability**: MCP enables swapping tools and LLMs in a plug-and-play manner, making integration easier.
2. **Two-Way Data Communication**: The LLM can both read from and send data to external systems via these connections.
3. **External Tools Integration**: MCP supports integration with file systems, GitHub, web scraping utilities, and other tools.
4. **Host Applications**: The Claude desktop app currently serves as the host application, which allows these integrations to function locally.
5. **Open-Source SDK**: SDKs for Python and TypeScript are available to build custom servers.

### Use Cases for MCP

1. **Code Management**: MCP can integrate with IDEs like VS Code to manage files, generate code, run tests, and more.
2. **Data Querying**: Integrate with Brave Search, GitHub, or any API-driven system to bring relevant data into the model context.
3. **Agent Development**: MCP enables building agents that act autonomously by utilizing a range of connected tools and services.

### Setting Up the Claude Desktop App and MCP Servers

1. **Install Claude Desktop**:
   - Available for Windows (including ARM64) and macOS.
   - Installation is straightforward, much like any desktop app.

2. **Locate and Configure the App**:
   - **On Mac**: The Claude app files are typically found in `~/Library/Application Support/Claude`.
   - **On Windows**: The files are found in `C:\Users\[Username]\AppData\Roaming\Claude`.

3. **Create Configuration File**:
   - Go to the directory where Claude is installed and create a new configuration file for MCP servers:
     ```bash
     cd ~/Library/Application Support/Claude
     touch config
     ```
   - Open this configuration file in your preferred IDE, such as VS Code or Cursor.

4. **Add MCP Server Information**:
   - Paste server information into the config file. Servers refer to the external scripts or APIs that Claude can call upon. These can include local scripts for tasks such as reading files, accessing GitHub repositories, and using Brave Search.

### Example: Adding Pre-built MCP Servers

1. **Using Pre-made MCP Servers**:
   - Anthropic has provided pre-built MCP servers, including:
     - **Brave Search**: Conducts web searches using the Brave API.
     - **File System Server**: Allows the LLM to read, write, and modify files on the local system.
     - **GitHub Server**: Facilitates reading and pushing to GitHub repositories.
     - **Web Scraper (Puppeteer)**: For browsing and scraping web data using the Puppeteer library.

2. **Access the GitHub Repository**:
   - The pre-built servers can be found in the GitHub repository linked in the documentation.

3. **Configure the Servers**:
   - Example: Setting up **Brave Search**.
     - Install the Brave MCP server:
       ```bash
       git clone https://github.com/anthropic/mcp-servers.git
       cd mcp-servers/brave
       npm install
       ```
     - Set up an API key for Brave Search as per the instructions provided in the documentation.
     - Edit the config file to include:
       ```json
       {
         "mcp_servers": {
           "brave_search": {
             "api_key": "YOUR_BRAVE_API_KEY"
           },
           "file_system": {},
           "puppeteer": {}
         }
       }
       ```

### Using MCP with Claude Desktop App

1. **Launch the Claude Desktop App**:
   - Once configured, launch the Claude app. You will see an option indicating the availability of multiple MCP tools.

2. **Run a Search**:
   - Example: Extracting Articles from VentureBeat:
     ```plaintext
     Ask the LLM: "Can you use puppeteer to extract titles from articles about Anthropic on VentureBeat?"
     ```
   - The app will prompt you to approve the use of specific tools (e.g., Puppeteer). After approval, it will browse the site and return the required data.

3. **Store Data Using File System Integration**:
   - You can instruct Claude to save the extracted information to a local text file by specifying the directory and file name. Each tool operation will require your permission.

### Developing Custom MCP Servers

1. **SDKs for Custom Servers**:
   - **Python SDK** and **TypeScript SDK** are available to create custom MCP servers.
   - The SDK documentation provides detailed examples to help you build and deploy these servers.

2. **Example in Python**:
   - Suppose you want to create a custom MCP server to interact with a local database. Start by installing the SDK:
     ```bash
     pip install anthro-mcp
     ```
   - Example code to build a server:
     ```python
     from anthro_mcp import MCPServer

     class CustomDatabaseServer(MCPServer):
         def handle_query(self, query):
             # Custom logic to interact with your database
             results = query_database(query)
             return results

     if __name__ == "__main__":
         server = CustomDatabaseServer()
         server.start()
     ```

### Conclusion

Anthropic’s **Model Context Protocol** represents a significant advancement in making LLMs versatile by connecting them to tools and external data systems. The protocol’s open standard approach and comprehensive integration options make it ideal for future agent-based systems. By following the guide above, you can start using MCP to improve how your LLM interacts with external data sources and even build your custom integrations for advanced use cases.

### Next Steps

1. **Explore the Available MCP Servers**: Install and test the pre-built servers to get comfortable with the setup.
2. **Try Creating a Custom MCP Server**: Use the SDK to create a server that fulfills a particular requirement—maybe one that interacts with a specific API or file system in a unique way.
3. **Experiment with Agent Integration**: Start thinking about how MCP can be used to create an intelligent agent that automates specific workflows by integrating multiple servers and tools.

Feel free to ask for more details or code examples about specific parts of the process—there's a lot of potential in this new technology, and I'd be happy to help you explore it further!

[[Claude Agents]]  [[LLM]]  [[Code Editor]]  [[Python]]  