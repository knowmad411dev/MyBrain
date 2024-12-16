---
tags:
- companion
---

## **Personal AI Assistant

This text is a transcript from a YouTube video by Zar, discussing how to create a comprehensive AI assistant using tools like Telegram, n8n, OpenAI, Airtable, and others. Below is a detailed summary, including instructions and code examples.

### Summary of Features and Workflow

1. **AI Assistant Overview**:

    - The AI assistant is highly capable, handling tasks like managing emails, updating databases, accessing calendars, retrieving tasks, and accessing the web, including Hacker News.
    - It can connect to private data via vector databases, making it a versatile AI agent that automates tasks, saves time, and minimizes hassle.

2. **Tools and Technologies Used**:

    - **Telegram**: Used as the primary communication interface, where users can interact via text or voice messages.
    - **n8n**: A no-code automation platform that integrates with various services.
    - **OpenAI**: Used for AI-based responses and transcription services.
    - **Airtable**: Acts as a database for storing contact information and tasks.
    - **SerpAPI**: For web searches.
    - **OpenWeatherMap API**: To access weather data.
    - **Vector Database (e.g., Pinecone)**: Used for secure access to sensitive data.

3. **Key Functionalities and Features**:

    - **Email Management**: Retrieves unread emails and summarizes them for the user.
    - **Database Interaction**: Uses Airtable to retrieve and update records. For example, retrieving contact information or adding new contacts.
    - **Calendar Management**: Can get and set calendar events.
    - **Web Access**: Retrieves information using Hacker News and SerpAPI.
    - **Voice and Text Commands**: Allows users to interact with the AI assistant via voice commands transcribed to text using OpenAI.
    - **Workflow Integration**: Custom tools and nodes integrated into n8n workflows to add various functionalities.

### Instructions and Code Examples

#### 1. Initial Setup with Telegram and n8n

- **Telegram Bot Setup**: Create a Telegram bot using the BotFather. The bot is used to send and receive messages between the user and the AI agent.
- **Telegram Node in n8n**:
    - **Trigger on Message**: The trigger listens for messages (text or voice) from Telegram.
    - **Voice to Text Conversion**: Voice messages are converted to text using the OpenAI node.
    - The following pseudocode explains the flow:

        ```python
        if message.type == 'voice':
            download_file(voice_message)
            transcribe(voice_message)  # Using OpenAI's transcription tool
            text = transcribed_message
        else:
            text = message.text
        ```

#### 2. Parsing Commands and Routing to Appropriate Tools

- **Switch Node** in n8n: A switch node is used to determine whether the incoming message is a text or voice message. Based on this, the workflow routes the message to either text handling or voice handling nodes.
- **Set Field Node**: Used to standardize the output format of the incoming message as `json.text`, regardless of whether it is a voice or text message.

#### 3. AI Agent Integration

- **Tools Agent Node in n8n**:
    - **Advanced Tools Agent**: An advanced agent is set up with multiple tools attached to it.
    - **Prompt Setup**: A comprehensive prompt is given to instruct the AI agent on how to use different tools based on user queries.
    - **Date Management**: Uses `now()` to get the current date, ensuring that the AI has a proper understanding of today’s date for scheduling and email tasks.
- **Prompt Example**:

    ```bash
    "You are a helpful assistant. For managing emails, use the Read Email tool to fetch unread emails. For database operations, use the Airtable tool as specified..."
    ```

#### 4. Attaching and Configuring Tools

- **Attaching Tools to n8n**:
    - **Email Management Tool**:
        - Reads emails using a Gmail tool node.
        - Filters for unread emails and uses a limit to manage the number of emails retrieved.
        - Example:

            ```python
            tool: read_email
            filters: { label: "inbox", read_status: "unread" }
            limit: 20
            ```

    - **Airtable Tool for Database Interaction**:
        - Retrieves contact information or creates new records.
        - The AI uses the `fromAI()` function to dynamically populate fields like name, email, and phone number.
        - Example for creating a contact:

            ```python
            name = fromAI('name')
            email = fromAI('email')
            phone = fromAI('phone')
            ```

#### 5. Example Workflow Demonstrations

- **Retrieving Unread Emails**:
    - The user asks, "Hi Mia, do I have any emails today?".
    - The system uses OpenAI to convert the voice to text, then reads emails using the Gmail tool and returns the unread emails.
- **Database Interaction**:
    - The user types, "Can you get me John Doe's contact information?".
    - The AI searches Airtable for John's contact information and provides it in the chat.
- **Weather Updates**:
    - The user asks, "What's the weather in San Francisco right now?".
    - The workflow uses the OpenWeatherMap API to fetch the weather and return it to the user.

#### 6. Advanced Features and Vector Database Integration

- **Vector Database Access**: Provides access to secure, private data using a Pinecone vector database or similar alternatives.
- **Memory for Contextual Conversations**:
    - A buffer memory node is added to allow the AI to remember the context of the conversation, making follow-up queries more fluid.
- **Buffer Memory Example**:

    ```python
    memory: {
        listen_for: 'incoming_events.first.json.message',
        respond_to: 'json.output'
    }
    ```

#### 7. Using Tools Dynamically

- **Tools Description and** `**fromAI()**` **Usage**:
    - The `fromAI()` function dynamically populates the required parameters, such as keywords for search queries or task instructions.
    - Example with Hacker News:

        ```python
        tool: hacker_news
        operation: 'get_many'
        amount: fromAI('amount')
        query: fromAI('search_query')
        ```

#### 8. Final Integration and Test Cases

- **Live Demo of Workflow**: The video demonstrates creating a new contact ("Robert King") and confirms the entry was successfully added to Airtable.
- **Fallback to SerpAPI**: In case Hacker News fails, the assistant uses SerpAPI to perform web searches.

#### 9. Workflow Templates and Community Support

- Zar’s School Community:
    - Provides templates and live sessions for building the AI agent.
    - Members have access to exclusive tools, daily calls, and live build sessions.

### Conclusion

This AI assistant project offers a comprehensive automation tool capable of handling multiple tasks efficiently. By utilizing no-code platforms like n8n, the assistant can integrate numerous services like email, databases, web searches, and more. The use of the `fromAI()` function allows the assistant to dynamically adapt to user requests, ensuring that tools are used efficiently. Telegram integration provides a simple user interface for text and voice commands, making the AI assistant practical for a wide range of personal and business applications.

If you want to build an AI assistant of your own, the steps include:

1. Set up the Telegram bot and integrate it with n8n.
2. Define the tools and workflows, using nodes to handle different services like email, databases, and weather.
3. Create a dynamic prompt to guide the AI assistant in understanding which tool to use for which task.
4. Test various functionalities like getting emails, accessing databases, adding records, and retrieving weather information.
5. Attach buffer memory for contextual conversation capabilities.
6. Utilize Zar's templates and community for additional support and resources.

```python
# Initial Setup with Telegram and n8n
if message.type == 'voice':
    download_file(voice_message)
    transcribe(voice_message)  # Using OpenAI's transcription tool
    text = transcribed_message
else:
    text = message.text

# Attaching and Configuring Tools

# Email Management Tool
# Reads emails using a Gmail tool node
# Filters for unread emails and uses a limit to manage the number of emails retrieved
tool = 'read_email'
filters = {
    'label': 'inbox',
    'read_status': 'unread'
}
limit = 20

# Airtable Tool for Database Interaction
# Retrieves contact information or creates new records
def create_contact():
    name = fromAI('name')
    email = fromAI('email')
    phone = fromAI('phone')
    return {
        'name': name,
        'email': email,
        'phone': phone
    }

# Memory for Contextual Conversations
memory = {
    'listen_for': 'incoming_events.first.json.message',
    'respond_to': 'json.output'
}

# Using Tools Dynamically
# Example with Hacker News
tool = 'hacker_news'
operation = 'get_many'
amount = fromAI('amount')
query = fromAI('search_query')

# Buffer Memory Example
buffer_memory = {
    'listen_for': 'incoming_events.first.json.message',
    'respond_to': 'json.output'
}

# Creating Contact with Airtable
def create_airtable_contact():
    contact = {
        'name': fromAI('name'),
        'email': fromAI('email'),
        'phone': fromAI('phone')
    }
    return contact

```

[[AI Companion]]