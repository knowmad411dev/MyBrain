---
tags:
- ollama
- python
video-url: https://www.youtube.com/watch?v=Jxt-coDVbR4&list=WL&index=6
---

## **Overview of Open Web UI Features: Tools, Filters, Functions, and Pipelines

### Introduction to Open Web UI Advanced Features

The text provides an in-depth walkthrough of advanced functionalities in Open Web UI, such as tools, filters, functions, and pipelines, that help users to expand the capabilities of large language models (LLMs). Each feature is explained, along with specific code examples and the usage of these elements to customize workflows effectively.

### Key Features Discussed

1. **Tools**: Custom Python functions that LLMs can optionally use.
2. **Filters**: Pre-processing or post-processing mechanics that control inputs and outputs to/from the LLM.
3. **Pipelines**: Workflows containing filters, custom functions, or entire workflows that can handle LLM inputs and outputs.
4. **Functions Tab**: Used to create filters and pipelines directly within Open Web UI without installing new Python packages.

### Tools

- **Definition**: Tools are essentially Python functions that extend LLM functionality by offering specific actions, such as calculations or information retrieval.
- **Usage**:
  - Tools are added via the admin interface of Open Web UI. Users need to create a new tool by clicking the "+" button under the workspace tab.
  - Example code for a tool involves defining Python classes and functions to specify the intended behavior.

#### Example: Date Tools

- **Functions Defined**:
  - `get_current_time`: Retrieves the current time.
  - `calculate_duration`: Calculates the time between two given dates.
  - `get_day_of_week`: Determines the day of the week for a given date.
- **Code Structure**:
  ```python
  class DateTools:
      def __init__(self):
          # Initialization code here

      def get_current_time(self):
          """ Returns the current time """

      def calculate_duration(self, start_date, end_date):
          """ Calculates the duration between two dates """
          
      def get_day_of_week(self, date):
          """ Returns the day of the week for a given date """
  ```

- **Adding Tools in Open Web UI**:
  - Navigate to the admin panel, select "Tools", click "+", and provide a description of each function.
  - The model needs to be properly equipped with the tool using the appropriate checkboxes.

### Filters

- **Definition**: Filters are used to process messages before or after they are passed to the LLM. They can modify the incoming query (inlet filter) or the response from the model (outlet filter).
- **Examples of Filter Use**:
  - Translating user input into English to improve model response.
  - Adjusting tone or removing unnecessary words from the model output.

#### Example: Prefixer Filter

- **Purpose**: Adds a prefix to the user input, e.g., "Create one stanza poem of".
- **Code Structure**:
  ```python
  class PrefixFilter:
      def __init__(self):
          self.prefix = "Create one stanza poem of"

      def inlet(self, message):
          # Adds a prefix to the incoming user message
          return self.prefix + message
  ```

- **How to Use**:
  - After creating the filter, it must be enabled in the model configuration under the functions tab.
  - It can be tested in a chat to see how user inputs are transformed.

### Pipelines

- **Definition**: Pipelines extend the capabilities of filters by allowing users to chain multiple operations, making them highly powerful for creating workflows involving multiple tools, agents, or external databases.
- **Use Cases**:
  - Querying external APIs.
  - Integrating multiple LLMs for complex workflows.
  - Adding additional agents to handle parts of the conversation.

#### Example: Basic Retrieval System

- **Purpose**: Demonstrates a simple pipeline for retrieving information from a pre-defined dictionary.
- **Code Structure**:
  ```python
  class BasicRetrievalPipeline:
      def __init__(self):
          self.data_dict = {
              "gesha": "A type of coffee with unique flavor notes.",
              "blue_mountain": "A popular coffee variety known for its mild flavor."
          }

      def pipe(self, message):
          if message in self.data_dict:
              return self.data_dict[message]
          else:
              return "Cannot find product in the database"
  ```

- **How to Use**:
  - Deploy this pipeline by adding the Python script to the Open Web UI pipelines folder and starting the server.
  - Once enabled, it can be selected for use in a new chat session.

### Functions Tab

- **Purpose**: Allows users to directly create filters or pipelines without the need for installing additional Python dependencies.
- **Limitation**: The scope of functionality is limited by the available libraries in the Open Web UI environment.
- **Usage**:
  - Navigate to the functions tab to add new filters or pipelines.
  - Modify the default template to define desired inlet/outlet behavior.

### Key Considerations and Observations

1. **Tool and Function Integration**:
   - Simply equipping a tool doesn't guarantee that the model will always use it. The tool must be explicitly enabled during a chat session.
2. **Model Behavior with Tools**:
   - Different models (e.g., GPT-4 vs. GPT-4-mini) exhibit different behaviors in terms of instruction following and tool usage. For instance, some tools like the "fortune teller" worked consistently, while others like "math calculations" failed due to model preferences.
3. **Pipeline Capabilities**:
   - Pipelines can be as simple as modifying user messages or as complex as integrating additional LLMs, agents, or accessing external databases.
   - Example usage includes interacting with a vector embedding database or running a custom retrieval system.

### Practical Example Walkthroughs

1. **Date Tool Example**:
   - Create a tool that performs date calculations.
   - Equip the tool to a GPT-4-mini model.
   - Enable the tool in the chat session to use functions like getting the day of the week.

2. **Pipeline Prefixer Example**:
   - Implement a filter to add prefixes to user messages.
   - Configure a model to use this filter and test the behavior in the chat.

3. **Retrieval Pipeline Example**:
   - Use a pipeline to look up information from a dictionary.
   - Chain the pipeline to a model that can then create a social media post based on the retrieved information.

### Conclusion

The walkthrough demonstrates how to use tools, filters, functions, and pipelines in Open Web UI to extend the functionality of LLMs effectively. It explains how each feature can be implemented using Python, how to equip these features in Open Web UI, and their different behaviors. Properly configuring these elements can significantly enhance the flexibility of interactions and enable custom workflows tailored to user needs.

---

This overview retains the practical information, providing a simplified explanation of the advanced features available in Open Web UI, with direct examples for how to apply them. If you'd like, I can dive deeper into any specific part or even provide a simplified guide on how to implement one of these tools or pipelines in your setup. Let me know how you'd like to proceed!

[[Open Web UI]]  [[Python]]