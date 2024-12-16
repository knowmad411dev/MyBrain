---
tags:
- companion
video-url: https://www.youtube.com/watch?v=3hdtfhCeBsg&list=WL&index=2
---

## **Build Jarvis

This appears to be a transcript from a YouTube video, where someone is explaining how they built an AI assistant modeled after "Jarvis" from Iron Man, using multiple AI tools and platforms to create a conversational AI with specific personality traits. Here's an overview of what they did, what you need, and the learning steps:

### **How Does It Work?**

1. **Core AI Agent & Tools**
   - The creator built a Jarvis-like AI assistant using a combination of different AI models and voice tools.
   - The AI responds to natural language queries and performs various tasks, like providing the weather, checking a calendar, accessing project management data, and more.
   - They use **n8n**, a low-code automation platform that connects different APIs and services, to orchestrate the various functions.
   - The AI agent has a main "prompt" that dictates which tool to use based on the input from the user. Essentially, it functions like a dialog manager to decide what action is required.

2. **Voice Synthesis with Eleven Labs**
   - The AI has a synthesized voice to mimic Jarvis’s voice, generated via **Eleven Labs**. Eleven Labs is an AI tool that allows for both voice cloning and voice synthesis.
   - This synthesized voice is generated and returned to the user after processing their query.

3. **Connected Tools**
   - **Telegram**: This AI assistant uses a Telegram integration to interact with the user via voice or text messages. Depending on the type of input, it routes the message for either text analysis or transcription.
   - **Project Management**: Airtable is used for managing contacts and to-do lists, and it is queried by the assistant for task-related information.
   - **Internet Access**: Tools like **SURF API** or **Hacker News** provide the assistant with internet connectivity to answer broader information-based queries.
   - **Memory and Context Management**: Memory is used to provide a more natural conversational experience by referencing earlier context.

4. **AI Personality with LLM Chains**
   - The assistant's personality (modeled after "Jarvis") is achieved using a "basic LLM chain" that contains a prompt providing the personality traits of Jarvis. It makes use of a large language model to generate responses with humor and wit, in line with the personality.

### **What Do You Need to Get Started?**

To replicate or understand the process of building such an AI assistant, here's what you need:

1. **Hardware and Software Tools**
   - **n8n Platform**: Install and learn to use n8n (an automation tool like Zapier but more flexible). This platform helps you create workflows that connect APIs and services.
   - **Telegram**: Set up a bot in Telegram. This will serve as the interface where the user can send queries and interact with the assistant.
   - **Eleven Labs Account**: You need an Eleven Labs account to generate and clone voices. You'll need to understand their API to connect this to your n8n workflows.
   - **HTTP Requests and APIs**: Some familiarity with making HTTP requests is necessary, particularly for connecting Eleven Labs API to n8n.

2. **Accounts and Services**
   - **OpenAI API**: Access to an AI model like GPT-3 or GPT-4 (OpenAI) to power the language understanding and personality responses.
   - **Airtable**: If you plan to include project/task management, sign up for Airtable or another project management service.
   - **SURF API**: A tool that can be used to provide internet browsing capabilities for live information searches.

3. **Programming Knowledge**
   - **Basic API Handling**: Understanding how to set up and manage APIs, including things like authentication, requests, and responses, is necessary.
   - **Automation Logic**: You need to be comfortable creating conditions, switches, and workflows to route different types of input (text vs. voice).

4. **Voice and Sound Tools**
   - **Voice Cloning and Synthesis**: Learn about voice cloning via Eleven Labs, as well as how to generate and work with audio files.
   - **Telegram Integration**: Understanding how to interact with Telegram API, especially to send and receive both voice and text messages.

### **Learning Path to Build Your Own AI Assistant**

1. **Learn About Automation Tools**: Familiarize yourself with **n8n**. You'll need to learn how to build workflows that include triggers, switches, and connecting different services. Their official documentation is a good place to start.
2. **Telegram Bot Development**:
   - Learn how to set up a **Telegram bot** using the BotFather on Telegram.
   - Get comfortable with Telegram APIs (sending text, voice messages, and retrieving messages).

3. **AI Models for Chat**:
   - Study how **OpenAI APIs** (or similar language models like Llama) work. This will be the core of making the assistant understand and respond intelligently.
   - Practice prompt engineering to ensure the assistant’s responses have a specific tone (like Jarvis).

4. **Voice Tools (Eleven Labs)**:
   - Get familiar with **Eleven Labs** for generating synthetic voices. You’ll need to understand how to use their API, which includes sending text and receiving audio files.
   - Experiment with voice cloning if you want to generate a unique voice for your assistant.

5. **APIs and HTTP Requests**:
   - Brush up on how to handle **REST APIs** using tools like Postman to understand how to call APIs, authenticate, and use JSON data.
   - Practice making **HTTP POST requests** for generating the audio from Eleven Labs and learn about handling JSON data within n8n.

6. **Python or JavaScript Basics**:
   - A bit of scripting may be necessary, especially for data processing or automation. Learn how to manipulate strings, work with JSON, and automate tasks with Python or JavaScript.

7. **Connecting Airtable or Other Data Tools**:
   - Sign up and learn **Airtable** if you want to include project management. Understand how to connect Airtable to other services using APIs.

8. **Building Personality with LLM Chains**:
   - To give your assistant a personality, you need to understand prompt chaining and personality prompts for language models.
   - Study how to create engaging and personality-driven prompts.

9. **Telegram and Workflow Integration**:
   - Learn about **n8n nodes**: Telegram trigger nodes, HTTP request nodes, and how to add custom authentication to keep things secure.
   - Practice creating routes that process either text or audio, handling transcription via OpenAI if needed.

### **Summary: Tools and Skills Needed**

- **Tools**:
  - n8n
  - Telegram
  - Eleven Labs (Voice Synthesis)
  - OpenAI API
  - Airtable (or other project management tool)
  - APIs (HTTP Requests)
- **Skills**:
  - **API Handling** (POST requests, authentication, etc.)
  - **Telegram Bot Development** (setup and integration)
  - **n8n Workflow Automation** (connecting different nodes)
  - **Voice Cloning and Synthesis**
  - **Prompt Engineering** for creating a personality
  - **Basic Scripting** (for JSON handling and automation)
  - **Familiarity with AI Model API calls** and utilizing them in a conversational flow.

If you're interested in building a Jarvis-like assistant, you will need a mix of the above technical tools, API integrations, and automation knowledge. If you need more specific guidance or detailed explanations on any of these topics, feel free to ask, and we can break it down further.

[[AI Companion]]
