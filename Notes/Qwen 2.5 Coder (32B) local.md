---
tags:
- editors
- ollama
---
## **Qwen 2.5 Coder (32B) Local

### Overview

The video discusses the new **32 billion parameter Quen 2.5 Coder Model** and compares it with **GPT-4.0** and **Claude 3.5 Sonnet**. It demonstrates how to run the model locally, using **Olama** and **Open Web UI**, and integrates it into **VS Code** using **Continue**. The video explores running the model with command-line interfaces (CLI), through a web UI, and how it works for coding tasks in Python, JavaScript, and Rust.

### Key Concepts

1. **Olama**: Similar to Docker for LLMs, Olama provides a runtime to easily download and run language models on Mac, Linux, etc. Models can be accessed without needing platforms like Hugging Face.
2. **Quen 2.5 Model**: Available in both **32 billion** and **7 billion** parameter versions. The video shows using these models for coding purposes and comparisons.
3. **Open Web UI**: This web interface offers a ChatGPT-style interface and allows connection to Olama models.
4. **VS Code & Continue**: Integration is shown using the **Continue** extension, which allows access to Olama models for tasks like autocompletion and chat-style interaction directly in VS Code.

### Getting Started

- **Download Olama**: Visit [alarm.com](https://alarm.com) and download the tool for your OS.
- **Install Models**:
  - Use CLI to download the models: `olama run quen 2.5 dcoder 32b` (or replace `32b` with `7B` for the smaller version).

### Model Usage Examples

1. **Command-Line Interface**:
   - Run Quen 2.5:
     ```bash
     olama run quen 2.5 dcoder 32b
     ```

     Type a prompt, such as:

     ```bash
     hello there
     ```
   - Ask for code generation:
     ```bash
     write me a Fibonacci function in Python
     ```
   - The output includes **iterative**, **recursive**, and **optimized recursive** approaches using **memoization**.

2. **Open Web UI Setup**:
   - Go to [openwebui.com](https://openwebui.com).
   - Run it locally with Docker:
     ```bash
     docker run -p 3000:3000 openwebui
     ```
   - Access via a browser: `localhost:3000`.
   - After signing up, interact with the Quen models.

3. **VS Code Integration Using Continue**:
   - Install the **Continue** extension from [continue.dev](https://continue.dev).
   - Open a Python script, e.g., `hello.py`, and use Continue for **autocompletion**:
     - **Fibonacci Function**:
       ```python
       def fib(n):
           # Autocompletion from Continue
           ...
       ```
   - Configuration (in `config.js`):
     ```json
     {
       "tab_autocomplete_model": "quen25-coder",
       "providers": "ollama",
       ...
     }
     ```

### Web Interface Interaction

- The **Open Web UI** serves a similar purpose to the command line, providing a more user-friendly interface.
- **Example Interactions**:
  - Generate a **Fibonacci Function**.
  - Request additional versions, e.g., **memoization**.

### Multi-Step Conversations and Further Examples

- The **Quen Model** supports multi-step commands.
- For example, generating unit tests for a given function:
  - Use **Pytest Framework**:
    ```bash
    python memo_test.py
    ```
  - The **32 billion parameter** model gives detailed responses but runs slower compared to the **7 billion parameter** version.

### Working with APIs and More Complex Tasks

1. **YouTube API Example**:
   - Generate a Python script that interacts with the **YouTube Data API v3**.
   - Rewrite the code as a **CLI** using the **Click library**:
     ```python
     @click.command()
     def fetch_video_data():
         ...
     ```
   - Run:
     ```bash
     python y.py --query "llama 3.2"
     ```

2. **React Application Example**:
   - Generate a **React app** that shows real-time clock updates:
     ```bash
     npx create-react-app real-time-clock
     ```
   - Modify to use **bun**:
     ```bash
     bun create real-time-clock
     ```
   - Sync the clock with an **Internet Time Service**.

3. **Adding AI Generated Image**:
   - Include a picture of a blinking **AI-generated donkey**:
     ```javascript
     // Example in React code using SVG
     ```

### Rust Example

- Create a **Hello World** Web Server using **Salvo**:
  ```rust
  use salvo::prelude::*;

  #[fn main()]
  async fn main() {
      let router = Router::new().handle(hello);
      Server::new(TcpListener::bind("127.0.0.1:7878")).serve(router).await;
  }
  async fn hello() -> &'static str {
      "Hello, World!"
  }
  ```
- The **Quen Model** did not perform well with Rust compared to **Claude**.

### Performance Comparisons

- **32 Billion vs. 7 Billion** Parameters:
  - **32 billion** parameter model provides more detailed responses but at slower speeds.
  - **7 billion** parameter model is faster and suitable for autocompletion and small tasks.
- **Claude 3.5 Sonnet** performed better in certain complex tasks, including API interactions and web server generation in Rust.
- **GPT-4.0** performed decently but sometimes lacked specific optimizations.

### Recommendations

- Use **Quen 2.5** with **Olama** for easy local deployment.
- Use **Open Web UI** for a user-friendly chat experience.
- Integrate with **VS Code** using **Continue** for coding assistance.
- Choose between **32 billion** and **7 billion** parameter models based on task requirements.
- Use **7 billion** parameter model for autocompletion and **32 billion** for detailed generation.

### Final Takeaway

The **Quen 2.5 Coder Model** is a powerful tool that can run locally, providing a high-quality coding experience with both small and large parameter models. While not on par with **Claude** or **GPT-4.0** in every aspect, it is a viable option for those who prefer local deployment without relying on cloud services.

[[Overview of Co-Pilot Arena and Setting It Up]]  [[AI Coding for Free]]  [[Free AI Tools]]  [[Python]]  [[Ollama]]  [[Code Editor]]