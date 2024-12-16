---
tags:
- ollama
- python
video-url: https://www.youtube.com/watch?v=QzRPtorrZVo&list=WL&index=2
---

## **Ollama Tool Calling: A Detailed Overview**

Ollama's native tools, also known as function calling, offer significant improvements for integrating custom functions or tools directly into language model workflows. This overview walks you through the latest updates to the Ollama Python library, highlighting how to create and integrate custom tools, use asynchronous operations, and leverage existing functions. Below, you'll find step-by-step instructions and the complete code to build your custom tools and seamlessly integrate them into the Ollama environment.

### **Why We Need Tools**

By default, large language models do not have access to real-time data. For instance, when asked, "What is the current stock price of Apple?" a standard model would respond, "I don't have real-time data." However, by introducing tools, you can enable function calling to retrieve real-time data.

For example, with function calling, a tool called `get_stock_price()` can fetch the stock price of Apple by passing the stock symbol "AAPL" to the function. The tool will retrieve the price, and the AI will be able to respond accurately, e.g., "The stock price of Apple is $235." The rest of this guide shows you how to create custom tools and integrate them with Ollama.

### **Step 1: Creating a Custom Tool**

1. **Install Required Packages**: Start by installing Ollama and Yahoo Finance.
   ```bash
   pip install ollama yahoo-finance
   ```

   Ollama is the main package for our language model, and Yahoo Finance will be used for retrieving stock prices.

2. **Download the Llama Model**: After installing the main package, download a specific model.
   ```bash
   olama pull llama 3.2
   ```

3. **Create the Application File**: Next, create a file called `app.py` and open it in your code editor. Here's how you can set it up:
   ```python
   import olama
   from yahoo_finance import Share
   from typing import Dict, Any, Callable

   # Define the function to get the stock price
   def get_stock_price(symbol: str) -> float:
       stock = Share(symbol)
       return stock.get_price()

   # Step 2: Integrate with Ollama
   def main():
       # Create an Ollama client
       client = olama.Client()

       # Define the tool
       tools = [
           {
               'name': 'get_stock_price',
               'func': get_stock_price,
               'description': 'Gets the current stock price of a given symbol.'
           }
       ]

       # Ask the question
       response = client.chat(
           model='llama 3.2',
           role='user',
           content='What is the current stock price of Apple?',
           tools=tools
       )

       # Parse the tool call and get the response
       if response.tool_call:
           function_name = response.tool_call.name
           args = response.tool_call.args
           result = get_stock_price(*args)
           print(f'The stock price of Apple is {result} USD.')

   if __name__ == '__main__':
       main()
   ```

### **Step 2: Using Asynchronous Operations**

You can also create asynchronous functions to handle operations concurrently.

1. **Install `asyncio` Library**:
   ```bash
   pip install asyncio
   ```

2. **Modify the Code for Async**:
   Here’s an example to add two numbers asynchronously:
   ```python
   import asyncio
   from typing import Dict, Any, Callable

   async def add_two_numbers(a: int, b: int) -> int:
       await asyncio.sleep(0)  # Simulate an async operation
       return a + b

   async def main():
       client = olama.AsyncClient()
       tools = [
           {
               'name': 'add_two_numbers',
               'func': add_two_numbers,
               'description': 'Adds two numbers asynchronously.'
           }
       ]
       response = await client.chat(
           model='llama 3.2',
           role='user',
           content='What is 3 + 1?',
           tools=tools
       )
       if response.tool_call:
           result = await add_two_numbers(3, 1)
           print(f'The result is {result}.')

   if __name__ == '__main__':
       asyncio.run(main())
   ```

   This code uses the `asyncio` library to manage asynchronous calls, allowing the function to add numbers without blocking the flow of the program.

### **Step 3: Using Existing Python Functions**

Another advantage of the Ollama tool integration is the ability to use existing Python functions.

1. **Using the Requests Library**:
   Python has many built-in libraries and third-party libraries that can be used as tools in Ollama.

2. **Example: Using `requests` to Fetch Web Data**:
   ```python
   import requests
   from typing import Dict, Any

   def fetch_webpage(url: str) -> str:
       response = requests.get(url)
       return response.text

   def main():
       client = olama.Client()
       tools = [
           {
               'name': 'fetch_webpage',
               'func': fetch_webpage,
               'description': 'Fetches the content of a given URL.'
           }
       ]
       response = client.chat(
           model='llama 3.2',
           role='user',
           content='Fetch the contents of https://example.com',
           tools=tools
       )
       if response.tool_call:
           result = fetch_webpage(response.tool_call.args[0])
           print(result)

   if __name__ == '__main__':
       main()
   ```

   This code allows Ollama to fetch and scrape webpage content by utilizing the existing `requests` library. The function `fetch_webpage()` is registered as a tool and can be invoked by the AI model.

### **Summary**

1. **Created Custom Tools**: Developed a `get_stock_price()` function to retrieve stock prices using Yahoo Finance.
2. **Asynchronous Tool Calls**: Learned how to create async functions using `asyncio` to make the application more efficient.
3. **Using Existing Libraries**: Leveraged existing Python functions, such as `requests`, to extend functionality without creating new tools from scratch.

This process allows you to integrate real-world data sources, custom logic, and asynchronous capabilities into Ollama, making your AI much more powerful and useful in handling specific tasks.

[[Ollama]]  [[Python]]