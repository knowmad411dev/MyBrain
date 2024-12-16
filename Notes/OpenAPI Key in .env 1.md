---
tags:
- openai
- vscode
- python
---

## **OpenAPI Key in .env

Step 1: Create a .env File

In your project directory, create a .env file and add your OpenAI API key.

The .env file should look like this:

OPENAI_API_KEY=your_openai_api_key_here

Step 2: Install the dotenv Package

Install the 'python-dotenv' package to load environment variables from the .env file

Command: pip install python-dotenv

Step 3: Load the Environment Variable in Your Code

import os

from dotenv import load_dotenv

Load environment variables from the .env file

load_dotenv()

Get the OpenAI API key

openai_api_key = os.getenv("OPENAI_API_KEY")

Example usage

import openai

openai.api_key = openai_api_key

Now, you can use the OpenAI API key securely in your code

 [[VSCode]]  [[Python]]  [[Code Editor]]   [[OpenAI How-to LLM Models]]