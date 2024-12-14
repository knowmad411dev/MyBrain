---
Video-URL: https://www.youtube.com/watch?v=ZgMDy2GWWU8&list=WL&index=1
tags:
- llm
- python
---

## **Promtech Python Library**

The video explains how to use a Python library called **Promptech**, which makes it easier to interact with Large Language Models ([[LLM]]s). The presenter walks through setting up and using the tool with another library, **LightLLM**, and demonstrates how to create prompts, handle input arguments, and receive structured outputs from LLMs.

### Key Components:

1. **What is Promptech?**

    - Promptech is a lightweight Python library that simplifies interactions with LLMs, making it easier for developers to create prompts and handle structured responses.
    - Promptech works on top of **LightLLM**, another library that allows you to interface with hundreds of different LLMs, either hosted locally or through APIs from various platforms like AWS Bedrock, Azure, OpenAI, Vertex AI, and others.

2. **Setup Overview:**

    - **LightLLM Installation**: First, LightLLM is installed. LightLLM provides the interface to interact with various LLMs.
    - **Promptech Installation**: Promptech is then installed, which utilizes LightLLM to simplify prompt handling.
    - The presenter uses a local LLM called **oLLama**, specifically the version **Llama 3.1**, to demonstrate Promptech. The oLLama model is quick to set up and can be installed by downloading an appropriate package for Linux, Windows, or MacOS.

3. **Setting Up the Environment:**

    - The presenter sets up a Python virtual environment to keep the packages isolated.

        ```
        python3 -m venv myenv
        source myenv/bin/activate
        ```

    - Once the environment is activated, **LightLLM** and **Promptech** are installed using `pip`.

        ```
        pip install lightllm promptech
        ```

4. **Using LightLLM Directly:**

    - The presenter first demonstrates how to use LightLLM to interact with a locally hosted model (oLLama):

        ```python
        import lightllm
        
        llm = lightllm.connect(model="llama-3.1", host="http://localhost:11443")
        response = llm.generate(prompt="Respond in 20 words, who are you?")
        print(response)
        ```

    - This connects to a local oLLama instance and sends a prompt to receive a response from the LLM.

5. **Using Promptech:**

    - The power of Promptech lies in its ability to create prompts easily with a decorator-based API. It simplifies the process of structuring prompts and outputs using function docstrings.

        ```python
        from promptech import llm
        
        @llm
        def who_was_president(year: int):
            """
            Respond with the name of the US president in the specified year.
            """
            return year
        
        response = who_was_president(2000)
        print(response)  
        # Output: "Bill Clinton"
        ```

    - The `@llm` decorator transforms the function to interact with the LLM. In this example, asking for the president in the year 2000 returns "Bill Clinton."

6. **Advanced Use with Pydantic:**

    - Promptech supports **Pydantic**, a popular library for creating structured data models with type checking and validation.

        ```python
        from pydantic import BaseModel
        from promptech import llm
        
        class CountryCapital(BaseModel):
            country: str
            capital: str
        
        @llm
        def get_capital(country: str) -> CountryCapital:
            """
            Given a country, return its capital.
            """
            return country
        
        response = get_capital("Ethiopia")
        print(response)  # Output: "CountryCapital(country='Ethiopia', capital='Addis Ababa')"
        ```

    - Using Pydantic allows for creating structured outputs, ensuring consistent format and reliability in responses from the LLM.

7. **Features of Promptech:**

    - **Decorator-Based API**: Simplifies the LLM interaction by abstracting the complexities of defining prompts.
    - **Streaming vs. Completion**: You can either receive real-time streaming responses or wait for full completion of the prompt.
    - **Integration with Pydantic**: Provides robust and type-checked data models for structured output.

### Installation and Usage Summary:

1. **Install Promptech and LightLLM**:

    ```
    pip install promptech lightllm
    ```

2. **Connect LightLLM to a local model (oLLama) or any other supported LLM.**

    ```python
    import lightllm
    llm = lightllm.connect(model="llama-3.1", host="http://localhost:11443")
    ```

3. **Use Promptech to Simplify LLM Interactions**:

    - Create simple functions using the `@llm` decorator.
    - Use Pydantic models for structured output when necessary.

### Resources:

- Promptech Documentation: Link to Promptech (placeholder for actual link)
- LightLLM Overview: Search the channel for in-depth tutorials and multiple perspectives on using LightLLM.
- GPU Rentals (by Mast Compute): Check out the sponsor for affordable GPU rentals with a 50% discount coupon provided in the video.

By using Promptech, developers can easily interact with LLMs by focusing on defining prompts and receiving structured responses with minimal code, streamlining the process of working with language models in Python.

[[Python]] [[LLM]]