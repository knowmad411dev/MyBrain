---
tags:
- agents
- google
- companion
---

## **How to Build a Chrome-Based Voice Assistant Using JavaScript APIs**

Working with models can enable the creation of powerful applications. However, there are several challenges, such as cost, latency, and data privacy. One potential solution is to utilize the user’s own device to handle simple tasks. The topic of on-device models is a broad one, which I won’t explore in depth here, but I encourage you to learn more about it. Instead, I’ll focus on a practical use case for this technology that you can build today: creating a voice assistant that runs entirely within Chrome.

I recently [published](https://medium.com/@kenzic/getting-started-window-ai-in-chrome-c2982efada33) an article about Chrome’s addition of the `window.ai` API in the developer build of the browser. This API is very new and highly experimental, but it demonstrates the interest from major tech companies and engineers in developing on-device models capable of handling simple tasks.

While writing that article, I started to wonder: could I create a voice assistant using only the APIs available in Chrome? The short answer is, yes!

**Before jumping in** If you’re not familiar with the Chrome `window.ai` API, I [suggest reading my article on the topic](https://medium.com/@kenzic/getting-started-window-ai-in-chrome-c2982efada33). You'll need to download the developer build of Chrome and enable a few flags. The article will guide you through the process step by step.

## Chrome APIs

Welcome back! Many of the voice assistants you’ve worked with operate using the following steps:

- Speech to Text
- LLM to process text and produce a text-based response
- Text to Speech

We’ll need a way to process each step and chain them together. Fortunately for us, Chrome ships with APIs that support each of these tasks.

## Speech to Text

For speech-to-text, we’ll use the WebKit Speech Recognition API, accessible via `window.webkitSpeechRecognition`. This API activates the user's microphone and provides functionality for voice detection and transcription. It also notifies us when the user stops speaking.

## LLM

Chrome has introduced Gemini Nano, an AI model designed for on-device use, along with an API for prompting it. You simply create a session, and pass your text prompt to session.prompt.

## Text to Speech

Once we have the text from the LLM, we’ll need a way to read it to the user. Chrome includes an API called `window.SpeechSynthesisUtterance`, which we can use to generate the spoken audio from text.

## Diving In!

> If you’re using VS Code, I recommend installing Live Server. This is what I’m using to run this code locally.

You can start by copying this template into your code editor. It contains the UI, but does not yet have the code to make this work. We’ll add this shortly!

```HTML
<html>
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Voice Assistant UI</title>
        <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
        <style>
            /* Custom animation for the speech bubble */
            @keyframes typing {
                0% {
                    transform: scale(1);
                    opacity: 0.7;
                }
                50% {
                    transform: scale(1.1);
                    opacity: 1;
                }
                100% {
                    transform: scale(1);
                    opacity: 0.7;
                }
            }
        </style>
    </head>

    <body class="flex items-center justify-center h-screen bg-gray-500">
        <div class="bg-black shadow-xl rounded-2xl p-6 w-80 space-y-4">
            <div class="text-center">
                <h1 class="text-2xl font-semibold text-white mt-2">Voice Assistant</h1>
            </div>

            <div class="flex items-center justify-center">
                <div id="assistant-bubble" class="hidden bg-white text-black p-3 rounded-2xl inline-block animate-pulse shadow-md" style="animation: typing 1s infinite;">
                    <span id="assistant-text">Listening...</span>
                </div>
            </div>

            <div class="flex justify-center">
                <button id="start" class="disabled:bg-gray-400 disabled:cursor-not-allowed bg-red-600 hover:bg-red-700 text-white font-medium py-2 px-6 rounded-full shadow-md transition duration-300 focus:outline-none">Start</button>
            </div>
        </div>

        <script>
            const assistantBubble = document.getElementById('assistant-bubble');
            const assistantText = document.getElementById('assistant-text');
            const startButton = document.getElementById('start');
            
            const showListening = () => {
                assistantBubble.classList.remove('hidden');
                assistantText.textContent = 'Listening...';
            }

            const showThinking = () => {
                assistantBubble.classList.remove('hidden');
                assistantText.textContent = 'Thinking...';
            }

            const hideBubble = () => {
                assistantBubble.classList.add('hidden');
                assistantText.textContent = '';
            }

            const textToSpeech = (text) => {
                const utterance = new window.SpeechSynthesisUtterance(text);
                window.speechSynthesis.speak(utterance);
            }

            const getSpeechToText = () => {
                const SpeechRecognition = window.webkitSpeechRecognition;
                const recognition = new SpeechRecognition();
                recognition.continuous = false;
                recognition.lang = 'en-US';
                recognition.interimResults = false;
                recognition.maxAlternatives = 1;
                return recognition;
            }

            const app = async function () {
                if ((await window.ai?.assistant.capabilities())?.available !== 'readily') {
                    alert('window.ai is not available in your browser');
                    return;
                }

                const session = await window.ai.assistant.create();

                startButton.onclick = function () {
                    startButton.disabled = true;
                    const recognition = getSpeechToText();

                    recognition.onresult = async function (event) {
                        const text = event.results[0][0].transcript;
                        showThinking();
                        console.log('Thinking...');
                        
                        const result = await session.prompt(text);
                        
                        hideBubble();
                        console.log('Speaking...');
                        textToSpeech(result);
                        
                        startButton.disabled = false;
                    };

                    recognition.onspeechstart = function () {
                        console.log('Speech has been detected');
                    };

                    recognition.onspeechend = function () {
                        console.log('Speech has stopped being detected');
                        recognition.stop();
                    };

                    recognition.onerror = function (event) {
                        console.error('Error occurred in recognition: ' + event.error);
                    };

                    showListening();
                    recognition.start();
                    console.log('Listening...');
                };
            }

            document.addEventListener('DOMContentLoaded', app);
        </script>
    </body>
</html>
```

First, we’ll setup a function that takes a string of text and converts it to audio. For this we’ll use the built-in Speech Synthesis API. Add this function below the comment `// Define textToSpeech and getSpeechToText functions:`

(JavaScript code for `textToSpeech` function.)

Next, let’s define a function that will return a speech recognition object:

(JavaScript code for `getSpeechToText` function.)

The recognition object has events that we can hook into. When the user finishes speaking, the `onresult` event is triggered, providing an event with the text transcript. We'll use this to send the text to the Gemini Nano and respond with spoken text. Add the following code below `// get speech to text, and handle the response`

(JavaScript code to handle `onresult` and other recognition events.)

In the app function, right below the comment `create a new session`, we'll want to start our session with Gemini Nano.

(JavaScript code to start a new session.)

Now that we have the necessary modules to build our app, we can dive into the `onresult` handler to write the business logic.

(JavaScript code for handling user speech input and generating responses.)

We’re almost there! We have everything we need to convert speech to text and respond with speech. Now, we just need to start the system listening. We can do this by activating speech recognition when the user clicks the “start” button:

(JavaScript code for `start` button interaction.)

## Using your voice assistant

If you’re using VS Code with Live Server, simply start the server and check out your awesome voice assistant. Click “start” and begin chatting away! It’s kind of like talking to Samantha from _Her_… okay, maybe not quite.

It’s still quite limited and nowhere near as advanced as voice assistants like ChatGPT, but that’s not the point. Using only the built-in APIs in your Chrome (dev) browser, you’ve created a functional, albeit basic, voice assistant with just a few lines of JavaScript.

The potential is enormous. The Google Gemini Nano model will likely improve as it’s integrated into the main browser build. Over time, we can expect to rely on this API for small and medium-sized tasks, only deferring to remote APIs for more complex tasks.

While I wouldn’t recommend using this in production just yet, I’m optimistic that you will be able to within the next year.

🔨 [You can find the complete source code on GitHub.](https://gist.github.com/kenzic/0029b92a726ac33b053689b7c4b86b03)

## Conclusion

That’s it for now! This was a quick and fun demo, but there’s so much more you can do. If you want to take it further, consider swapping out Gemini Nano for a different model. Check out my article on running open-source [models directly in your browser](https://medium.com/@kenzic/run-models-in-the-browser-with-transformers-js-2d0983ba3ce9). I’m hopeful we’re just seeing the beginning of on-device models which are accessible via JavaScript!

You could also enhance the assistant’s voice or make the conversation flow more naturally. See if you can push the limit when it comes to building on-device applications with Chrome’s built-in APIs. Have fun experimenting and pushing the boundaries of what’s possible!

 [[AI Voice Assistants]]