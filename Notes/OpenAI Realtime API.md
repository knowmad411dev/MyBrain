---
tags: 
- openai
- speech
video-url: https://www.youtube.com/watch?v=3wMGnzBrVsw&list=WL&index=32
---

## **OpenAI Realtime API**

### **Summary of Integrating OpenAI's Real-Time API for an AI Voice Assistant**

OpenAI has recently launched its **Real-Time API**, enabling developers to integrate a human-sounding AI voice assistant into custom applications. This API facilitates real-time, two-way audio conversations, making it ideal for applications such as an AI concierge for Airbnb guests. Below is a comprehensive summary, including related links, how-to instructions, and example code to help you get started.

---

#### **1. Introduction to OpenAI's Real-Time API**

OpenAI's Real-Time API allows developers to embed sophisticated AI voice assistants into applications. These assistants can handle natural conversations, provide detailed information about specific contexts (e.g., property details for Airbnb), and offer personalized recommendations. The API leverages WebSocket technology for seamless, real-time communication between the client and OpenAI servers.

**Key Features:**

- **Human-like Conversations:** Natural and engaging interactions.
- **Contextual Knowledge:** Deep understanding of specific topics (e.g., property details).
- **Real-Time Communication:** Instant data transfer using WebSockets.
- **Voice Activity Detection (VAD):** Enables natural turn-taking in conversations.

---

#### **2. Building an Airbnb AI Concierge Application**

The primary use case discussed involves creating an AI concierge for Airbnb guests. This assistant can provide information such as Wi-Fi passwords, locations of water shut-offs, and host recommendations for local restaurants. The application enhances guest experience by offering instant support without the need to contact the host directly.

---

#### **3. Using the OpenAI Real-Time Console Sample Application**

OpenAI has released a sample application called the **Real-Time Console**, which serves as an excellent reference for building custom applications using the Real-Time API. You can access the sample code on GitHub:

🔗 **GitHub Repository:** [OpenAI Real-Time Console](https://github.com/openai/realtime-console)

_Note: Ensure you have access to the Real-Time API beta and obtain your API key from OpenAI._

---

#### **4. Step-by-Step How-To Instructions**

##### **a. Setting Up the Environment**

1. **Clone the Sample Repository:**

    ```
    git clone https://github.com/openai/realtime-console.git
    cd realtime-console
    ```

2. **Install Dependencies:** Ensure you have Node.js and npm installed. Then run:

    ```
    npm install
    ```

3. **Import the Real-Time Client:** In your JavaScript file, import the Real-Time client from OpenAI's library:

    ```
    import { RealTimeClient } from 'openai-realtime-api-beta';
    ```

##### **b. Instantiating the Real-Time Client**

There are two ways to instantiate the Real-Time client:

1. **Using a Local Relay Server (Recommended):** This method is secure and recommended for production environments.
2. **Quick Setup (For Development):**

    ```
    const client = new RealTimeClient({
      apiKey: 'YOUR_API_KEY',
      dangerouslyAllowApiKeyInBrowser: true, // Use only for development
    });
    ```

_Warning:_ Storing API keys in the browser is insecure and should **only** be used for quick testing.

##### **c. Initializing the Session**

Set up the session with instructions and configurations:

```
client.updateSession({
  instructions: "Aloha and welcome to Pacific Horizon Condo. I'm Kai, your AI concierge. Ask me anything.",
  inputAudioTranscription: true,
  model: 'whisper-1',
  aiVoice: 'Shimmer',
});
```

##### **d. Handling Real-Time Events with WebSockets**

OpenAI uses WebSockets to maintain an open connection for instant data transfer. Implement event handling using the `on` method:

```
client.on('message', (data) => {
  // Handle incoming messages
});
```

##### **e. Managing Conversation Modes**

The Real-Time API offers two modes:

1. **Manual Mode:**

    - **Push-to-Talk:** Users manually initiate speaking.
    - **Implementation:**

        ```
        client.updateSession({ conversationType: 'manual' });
        ```

2. **Voice Activity Detection (VAD) Mode:**

    - **Natural Turn-Taking:** The system detects when the user starts and stops speaking.
    - **Implementation:**

        ```
        client.updateSession({ conversationType: 'server_vad' });
        ```

##### **f. Integrating Audio Input and Output**

Utilize utility functions provided in the GitHub package for handling audio:

```
import { WaveRecorder, WaveStreamPlayer } from 'openai-realtime-utils';

const recorder = new WaveRecorder();
const player = new WaveStreamPlayer();

recorder.begin();
player.connect();

// Send user message
client.sendUserMessage("Hey Kai, what's the Wi-Fi password?");
```

---

#### **5. Example Application Flow**

1. **Connect to the API:**

    ```
    client.connect();
    ```

2. **Initialize the Session with Property Details:** Include all relevant information about the Airbnb property to ensure the AI can respond accurately.

    ```
    client.updateSession({
      instructions: "Aloha and welcome to Pacific Horizon Condo. I'm Kai, your AI concierge. Ask me anything about the property.",
      // Additional property details here
    });
    ```

3. **Start Conversation:**

    - **Manual Mode Example:**
        - User: "Hey Kai, what's the Wi-Fi password?"
        - AI: "The Wi-Fi password is Aloha23. Happy surfing!"
    - **VAD Mode Example:**
        - User: "I have a flood issue."
        - AI: "I'm sorry to hear that. The main water shut-off is located in the hallway closet behind the beach towels. If you need further assistance, contact the property manager at 808-555-8572."

---

#### **6. Cost Considerations**

Using the Real-Time API can be **expensive**, with each brief conversation costing approximately **$0.25**. It's crucial to:

- **Set API Usage Limits:** To prevent unexpected high costs during development and testing.
- **Monitor Usage:** Regularly check your OpenAI dashboard to track API consumption.
- **Optimize Conversations:** Reduce unnecessary API calls by optimizing how the assistant handles queries.

_Note:_ OpenAI may reduce API prices over time as the service matures.

---

#### **7. Conclusion and Next Steps**

The Real-Time API by OpenAI offers powerful capabilities for creating interactive AI voice assistants. While it's currently in beta with some limitations (e.g., occasional sentence cut-offs), its potential for transforming customer service and enhancing user experiences is significant.

**Next Steps:**

- **Experiment with the Sample Application:** Clone and run the Real-Time Console to understand its functionalities.
- **Customize the AI Assistant:** Tailor the instructions and knowledge base to fit your specific application needs.
- **Implement in Production:** Once satisfied with testing, integrate the Real-Time API into your live applications, ensuring security best practices.

---

#### **Related Links and Resources**

- **OpenAI Real-Time API Documentation:** [https://beta.openai.com/docs/realtime-api](https://beta.openai.com/docs/realtime-api)
- **GitHub Sample Application:** [https://github.com/openai/realtime-console](https://github.com/openai/realtime-console)
- **OpenAI API Pricing:** [https://openai.com/pricing](https://openai.com/pricing)
- **Wave Recorder and Player Utilities:** Included in the GitHub repository's utility functions.

---

#### **Example Code Snippet**

Here's a simplified example to illustrate setting up the Real-Time client and handling a basic conversation:

```
import { RealTimeClient } from 'openai-realtime-api-beta';
import { WaveRecorder, WaveStreamPlayer } from 'openai-realtime-utils';

// Instantiate the Real-Time client
const client = new RealTimeClient({
  apiKey: 'YOUR_API_KEY',
  dangerouslyAllowApiKeyInBrowser: true, // Use with caution
});

// Initialize the session
client.updateSession({
  instructions: "Aloha and welcome to Pacific Horizon Condo. I'm Kai, your AI concierge. Ask me anything.",
  inputAudioTranscription: true,
  model: 'whisper-1',
  aiVoice: 'Shimmer',
});

// Handle incoming messages
client.on('message', (data) => {
  console.log('AI Response:', data.text);
  // Play AI response audio
  player.play(data.audio);
});

// Setup audio utilities
const recorder = new WaveRecorder();
const player = new WaveStreamPlayer();

recorder.begin();
player.connect();

// Connect to the Real-Time API
client.connect();

// Example user message
client.sendUserMessage("Hey Kai, what's the Wi-Fi password?");
```

_Ensure you replace_ `_'YOUR_API_KEY'_` _with your actual OpenAI API key and handle API keys securely in production environments._

---

By leveraging OpenAI's Real-Time API, developers can create highly interactive and intelligent voice assistants tailored to specific applications, enhancing user engagement and streamlining information delivery.

[[OpenAI]] [[AI Agents]]