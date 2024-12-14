---
tags:
- ollama
- editors
- cloud
video-url: https://www.youtube.com/watch?v=3tkmnItNXJM&list=WL&index=2
---
## **How to Run Ollama in Google Colab

## Step 1: Access Google Colab

1. Go to [Google Colab](https://colab.research.google.com/).
2. Sign in with your Google account if prompted.

---

## Step 2: Configure Runtime

1. In Google Colab, click on the **Runtime** menu.
2. Select **Change runtime type**.
3. Choose **GPU** as the hardware accelerator (preferably T4 GPU for optimal performance).

---

## Step 3: Install Required Packages

Run the following code in a Colab cell to install and set up Ollama:

```python
# Update the environment and install necessary packages
!sudo apt-get update
!sudo apt-get install -y pciutils

# Install Ollama
!pip install ollama

# Verify GPU setup using pciutils
!nvidia-smi
```

---

## Step 4: Handle Background Service with Subprocess

Google Colab executes code cells sequentially, which poses a challenge for running parallel services like Ollama. Use a Python subprocess to create a background service for Ollama:

```python
import subprocess
import time

# Start Ollama service in the background
ollama_service = subprocess.Popen(["ollama", "serve"], stdout=subprocess.PIPE, stderr=subprocess.PIPE)

# Add a delay to ensure the service is ready
time.sleep(5)
print("Ollama service is running.")
```

---

## Step 5: Download and Load a Model

Choose a model from the Ollama platform. For this guide, we'll use "Llama 3.2" as an example:

```python
# Download the Llama 3.2 model
!ollama pull llama:3.2

print("Model downloaded successfully.")
```

---

## Step 6: Integrate Ollama with LangChain

LangChain provides tools to build AI-powered applications using LLMs. Use the following code to integrate LangChain with Ollama:

```python
from langchain.prompts import PromptTemplate
from langchain.chains import LLMChain
from langchain.llms import Ollama

# Define the prompt template
prompt = PromptTemplate(template="What is happiness?", input_variables=[])

# Initialize the Ollama LLM
llm = Ollama(model="llama:3.2")

# Create a LangChain
chain = LLMChain(prompt=prompt, llm=llm)

# Run the chain and get the response
response = chain.run()
print("Response:", response)
```

---

## Step 7: Monitor Resource Usage

Use the following Colab feature to monitor system resources:

1. Click on the "View resources" button in the top-right corner of the Colab interface.
2. Verify that the GPU memory usage is reasonable (e.g., <15 GB).

---

## Optional: Save and Share

- To save your Colab notebook:
  1. Click **File > Save a copy in Drive**.
  2. Share the notebook link if needed.

---

## Summary

- You now have Ollama installed and running on Google Colab, with a downloaded model.
- The service runs in the background using a Python subprocess.
- LangChain is integrated for easy interaction with the LLM.

Feel free to explore other models and applications using Ollama and LangChain.

[[Ollama]]  [[LangChain]]  [[Python]]