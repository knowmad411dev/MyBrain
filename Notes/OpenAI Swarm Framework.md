---
tags:
- openai
video-url: https://www.youtube.com/watch?v=HF3gLMI18jg&list=WL&index=12
---

## **OpenAI Swarm Framework**

## Overview of Swarm: Multi-Agent Framework by OpenAI

**Swarm** is a newly released multi-agent framework from OpenAI. It enables **multiple agents to collaborate** on complex tasks, offering **lightweight, controllable, and beginner-friendly automation**. In this system, agents (like a manager, weather, and stock price agent) communicate with each other and perform specific tasks, e.g., fetching weather data or stock prices. This guide walks through building such a framework using Swarm.

---

## Key Features of Swarm

- **Agent Coordination:** Multiple agents (e.g., weather, stock price agents) collaborate seamlessly.
- **Customizable Tools:** Each agent can integrate specific tools (e.g., a weather tool or stock price tool).
- **Simple Installation and Usage:** You can install and use it with Python easily, even for beginners.
- **Transparency & Flexibility:** You can clearly see and modify all steps in the agent interactions.
- **Free to Use Locally:** Works with open-source models without relying on external dependencies like LangChain.

---

## Step-by-Step Implementation of Swarm Agents

### **1. Installation**

In your terminal, run the following commands to install Swarm and related dependencies:

```
pip install swarm yahoo_fin
```

- `**swarm**`: The core library for the multi-agent framework.
- `**yahoo_fin**`: Used to fetch stock prices from Yahoo Finance.

---

### **2. Set Up API Keys**

1. **OpenAI API Key**: Generate a key from the [OpenAI website](https://platform.openai.com/). Run the following to export it:

    ```
    export OPENAI_API_KEY='your_openai_api_key'
    ```

2. **OpenWeather API Key**: Create an account on the [OpenWeather website](https://openweathermap.org/) and get your API key. Export it as follows:

    ```
    export OPENWEATHER_API_KEY='your_openweather_api_key'
    ```

---

### **3. Create** `**app.py**` **for Your Agents**

#### Import Required Libraries:

```python
import os
import requests
from swarm import Swarm, Agent
```

#### Initialize the Swarm Client:

```python
client = Swarm()
```

#### Set Up Weather Tool:

```python
def get_weather(city):
    api_key = os.getenv('OPENWEATHER_API_KEY')
    url = f"http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}&units=metric"
    response = requests.get(url)
    data = response.json()
    if response.status_code == 200:
        return f"The weather in {city} is {data['main']['temp']}\u00b0C with {data['weather'][0]['description']}."
    return "Unable to fetch weather data."
```

#### Set Up Stock Price Tool:

```python
from yahoo_fin import stock_info

def get_stock_price(ticker):
    try:
        price = stock_info.get_live_price(ticker)
        return f"The current stock price of {ticker} is ${price:.2f}."
    except:
        return "Unable to fetch stock data."
```

---

### **4. Create the Manager and Agent Functions**

#### Define Manager Agent:

```python
manager_agent = Agent(
    name="Manager",
    instruction="Direct users to the correct assistant based on their query."
)
```

#### Define Weather Agent:

```python
weather_agent = Agent(
    name="WeatherAgent",
    instruction="Provide weather information.",
    tool=get_weather
)
```

#### Define Stock Price Agent:

```python
stock_price_agent = Agent(
    name="StockPriceAgent",
    instruction="Provide stock price information.",
    tool=get_stock_price
)
```

---

### **5. Configure Manager to Route Requests**

```python
def route_to_agent(query):
    if "weather" in query:
        return weather_agent
    elif "stock price" in query:
        return stock_price_agent
    return None
```

---

### **6. Run the Application**

```python
if __name__ == "__main__":
    query = input("Enter your query: ")
    selected_agent = route_to_agent(query)
    if selected_agent:
        response = selected_agent.run(query)
        print(response)
    else:
        print("No suitable agent found.")
```

---

### **7. Test the Application**

1. Save the code as `app.py`.
2. Run the script in your terminal:

    ```
    python app.py
    ```

3. Test with sample queries:

    - "What's the weather in New York?"
    - "What is the stock price of Apple?"

---

## How Swarm Compares with Other Frameworks

- **Crew AI / Autogen / LangChain**: These frameworks offer more mature tools for multi-agent systems.
- **Swarm’s Strengths**:
    - Lightweight and transparent.
    - Does not rely on complex libraries like LangChain.
    - Provides clear customization of every interaction step.
- **Swarm’s Current Limitation**: Still in the experimental phase and lacks some features available in Crew AI or Autogen.

---

## Conclusion

Swarm offers a **simple yet powerful framework** for building multi-agent systems. While it’s still not as feature-rich as competitors like Crew AI or LangChain, it’s a great choice for users who need **transparent and customizable** automation tools. With just a few lines of code, you can create agents to handle various tasks such as fetching weather data or stock prices.

[[OpenAI]]  [[Python]]