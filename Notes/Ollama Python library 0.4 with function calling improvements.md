---
tags:
- ollama
- python
---
## **Ollama Python library 0.4 with function calling improvements

In the latest version of the [Ollama Python library](https://github.com/ollama/ollama-python), functions can now be provided as tools. The library now also has full typing support and [new examples](https://github.com/ollama/ollama-python/tree/main/examples) have been added.

## Get started

Start by installing or upgrading the Ollama Python library:

```
pip install -U ollama
```

## Passing Python functions as tools

### Define a Python function

Start by defining a regular Python function. For better results, annotate parameter and return values types and optionally add a [Google-style docstring](https://google.github.io/styleguide/pyguide.html#doc-function-raises):

```py
def add_two_numbers(a: int, b: int) -> int: """ Add two numbers Args: a: The first integer number b: The second integer number Returns: int: The sum of the two numbers """ return a + b
```

### Pass the function as a tool to Ollama

Next, use the `tools` field to pass the function as a tool to Ollama:

```py
import ollama response = ollama.chat( 'llama3.1', messages=[{'role': 'user', 'content': 'What is 10 + 10?'}], tools=[add_two_numbers], # Actual function reference )
```

### Call the function from the model response

Use the returned tool call and arguments provided by the model to call the respective function:

```py
available_functions = { 'add_two_numbers': add_two_numbers, } for tool in response.message.tool_calls or []: function_to_call = available_functions.get(tool.function.name) if function_to_call: print('Function output:', function_to_call(**tool.function.arguments)) else: print('Function not found:', tool.function.name)
```

### Pass existing functions as tools

Functions from existing Python libraries, SDKs, and elsewhere can now also be provided as tools. For example, the following code passes the `request` function from the `requests` library as a tool to fetch the contents of the Ollama website:

```python
import ollama import requests available_functions = { 'request': requests.request, } response = ollama.chat( 'llama3.1', messages=[{ 'role': 'user', 'content': 'get the ollama.com webpage?', }], tools=[requests.request], ) for tool in response.message.tool_calls or []: function_to_call = available_functions.get(tool.function.name) if function_to_call == requests.request: # Make an HTTP request to the URL specified in the tool call resp = function_to_call( method=tool.function.arguments.get('method'), url=tool.function.arguments.get('url'), ) print(resp.text) else: print('Function not found:', tool.function.name)
```

### How it works: generating JSON Schema from functions

The Ollama Python library uses Pydantic and docstring parsing to generate the JSON schema. As an example, for the `add_two_nubmers` function declared at the start of this post, the following JSON schema is generated (and was previously required to be provided manually as a tool):

```json
{ "type": "function", "function": { "name": "add_two_numbers", "description": "Add two numbers", "parameters": { "type": "object", "required": [ "a", "b" ], "properties": { "a": { "type": "integer", "description": "The first integer number" }, "b": { "type": "integer", "description": "The second integer number" } } } } }
```

### Additional improvements to the Ollama Python library

The 0.4 release of the Ollama Python library includes additional improvements:

-   Examples have been updated on the [Ollama Python GitHub](https://github.com/ollama/ollama-python/tree/main/examples).
-   Full typing support throughout the library to support direct object access while maintaining existing functionality.

[[Ollama]]  [[Python]]