---
tags: 
- gpt
---

## **TOP APIs for Free

**Summary of How to Access Top AI Models for Free via GitHub**

The video discusses a method to access popular AI models, including GPT-4.0, for free by using the GitHub Marketplace. Here’s a detailed step-by-step guide for accessing these models:

1. **Accessing GitHub Marketplace**:

    - Go to the GitHub Marketplace, which has a section for AI models. You can search for "AI Models" or directly follow the provided link in the video description.
    - The models available for free include GPT-4.0, GPT-4.0 Mini, Llama 3.2, and Mistro. These models are hosted by various providers, including Microsoft Azure. Note that for newer models like the 01 series, you might need to join a waiting list, depending on availability.
    - Ensure that you are logged in to your GitHub account before proceeding. A free GitHub account is sufficient, and you do not need to provide any credit card information.

2. **Obtaining an API Key**:

    - After logging into your GitHub account, locate the link to request a developer key for the desired model. This link is typically provided on the model's page in the GitHub Marketplace.
    - Click on the link and select "Create New Token." You will be prompted to use the "class" option, which simplifies the token creation process.
    - Leave the "Select Scopes" section completely blank. This is important because the token is used only to identify which GitHub account is accessing the API, and no additional permissions are needed.
    - Click "Generate Token." A new token will be generated—copy and store this token securely, as it will not be shown again.

3. **Using the API Key in an Application**:

    - Once you have the API key, add it to your existing application. Depending on the language and framework you are using, there are different methods for integrating the key.
    - Go to the GitHub-provided playground for the model you want to use. The playground provides an interface to interact with the model and includes code snippets in various programming languages, such as JavaScript, Python, and C.
    - Click on the "Code" button in the playground to see sample code for making API requests. This sample code demonstrates how to use the API key to connect to the model.
    - The generated code uses the OpenAI packages, making it compatible with existing OpenAI workflows. The only key difference is that the base URL for the API is different. It points to an Azure-hosted endpoint, which is required to access the GitHub-provided models.
    - Adjust the sample code as needed, incorporating the API key and setting the base URL for your requests. If you are using JavaScript, for instance, the base URL will be provided in the code snippet, and you simply need to replace it in your application.

4. **Implementing Changes in an Existing Application**:

    - The video’s author demonstrates how to update an existing application that previously connected to models like Gro and Llama 3.2.
    - First, replace the existing API key with the new GitHub token. Ideally, you should store this token as an environment variable to enhance security and prevent hardcoding sensitive information.
    - Update the endpoint URL to point to the Azure-hosted endpoint as indicated in the GitHub-provided code. The endpoint URL can be found in the playground’s code snippet.
    - Update the model number to the desired one, such as GPT-4.0. This allows you to specify which version of the model you are using.
    - The rest of the application code remains largely unchanged, as the OpenAI packages are still being used. This makes the integration process smooth and easy, allowing you to quickly switch between paid OpenAI services and the GitHub-hosted versions.

5. **Running the Application**:

    - After making the necessary changes, you can run the application to test it. In the video, the author tests it by asking a question about a solar panel.
    - The application sends the request to GPT-4.0 via the updated Azure endpoint, and the response is returned just like in the original setup.
    - The author notes that all custom features of their application, such as response formatting and specific instructions, continue to function without any additional modifications. This is because the underlying logic and packages remain consistent.
    - This setup is highly beneficial for prototyping, as it allows developers to experiment with different AI models without any upfront cost.

6. **Usage Limits**:

    - Models accessed via GitHub Marketplace come with certain usage limits. For instance, the GPT-4.0 model has a limit of 50 requests per day. While this may not be sufficient for production applications, it is ideal for experimentation and prototyping purposes.
    - If you need fewer restrictions and higher request limits, consider using other models like Gro. Gro offers faster response times and higher usage limits, making it more suitable for continuous development and testing.
    - The author mentions that they have previously created content about using Gro for similar purposes, highlighting its benefits in terms of speed and request volume.

7. **Best Practices**:

    - Always use environment variables to store sensitive information like API keys. This practice not only secures your tokens but also makes it easier to manage different environments (e.g., development, testing, production).
    - Regularly check the GitHub Marketplace for updates on new models or changes to existing models. Availability and features may change, including the introduction of waiting lists for popular or newly released models.
    - Make sure to review the documentation provided with each model to understand specific capabilities, usage limits, and integration details.

The video provides a comprehensive solution for developers interested in experimenting with different AI models without incurring any financial cost. By leveraging the GitHub Marketplace and the provided API keys, you can easily integrate these models into your existing applications, making it a valuable resource for prototyping and learning.

[[AI Agents]]  [[AI Coding for Free]]  [[AI Coding Assistants]]  [[GitHub]]