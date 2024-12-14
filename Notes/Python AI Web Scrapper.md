---
Video-URL: https://www.youtube.com/watch?v=Oo8-nEuDBkk&list=WL&index=14
tags:
- python
- web
url: https://github.com/techwithtim/AI-Web-Scraper
---

## **[[Python]] AI [[Web Scrapping]]**

Building an AI Web Scraper with Python: A Comprehensive Guide

In this tutorial, you'll learn how to build an AI-powered web scraper using Python. The application leverages several powerful libraries and services to scrape, parse, and analyze data from any website.

---

### Overview

This tutorial walks you through building an AI web scraper capable of extracting data from any website. Key functionalities include:

- **User Interface:** Built with Streamlit for easy interaction.
- **Web Scraping:** Implemented using Selenium to automate browser actions.
- **Handling Restrictions:** Utilizes Bright Data to bypass IP bans and CAPTCHAs.
- **Data Parsing:** Cleans and processes HTML content with BeautifulSoup.
- **AI Integration:** Employs LangChain and LLaMA (an open-source language model) to analyze and structure the scraped data.

---

### Prerequisites

Before starting, ensure you have the following:

- Python 3.x installed
- Visual Studio Code (or another code editor)
- Basic knowledge of Python
- Familiarity with command-line operations

---

### Project Setup

#### 1. Create and Activate a Virtual Environment

**On Mac/Linux:**

```
python3 -m venv env
source env/bin/activate
```

**On Windows (CMD):**

```
python -m venv env
env\Scripts\activate
```

**On Windows (PowerShell):**

```
python -m venv env
.\env\Scripts\Activate.ps1
```

#### 2. Install Dependencies

- Clone or download the `requirements.txt` from the GitHub repository linked in the video description.
- Create a new `requirements.txt` file in your project directory.
- Install dependencies:

```
pip install -r requirements.txt
```

**Key Dependencies:**

- **Streamlit** for the web UI
- **Selenium** for browser automation
- **BeautifulSoup** for HTML parsing
- **LangChain** for language model integration
- **LLaMA** for AI processing
- **Bright Data** for handling IP bans and CAPTCHAs

---

### Creating the Streamlit User Interface

1. Create `main.py`:

```python
import streamlit as st

st.title("AI Web Scraper")

# Input box for website URL
url = st.text_input("Enter a website URL:")

# Button to initiate scraping
if st.button("Scrape Site"):
    st.write("Scraping the website...")
    # Placeholder for scraping functionality
```

2. Run the app:

```
streamlit run main.py
```

---

### Implementing Web Scraping with Selenium

1. Create `scrape.py`:

```python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
import time

def scrape_website(url):
    print("Launching Chrome browser...")
    chrome_driver_path = "./chromedriver"
    options = webdriver.ChromeOptions()
    service = Service(chrome_driver_path)
    driver = webdriver.Chrome(service=service, options=options)
    try:
        driver.get(url)
        print("Page loaded.")
        time.sleep(10)
        html = driver.page_source
        return html
    finally:
        driver.quit()
```

2. Download ChromeDriver from ChromeDriver Downloads.
3. Update `main.py` to use `scrape.py`:

```python
from scrape import scrape_website

if st.button("Scrape Site"):
    st.write("Scraping the website...")
    html_content = scrape_website(url)
    st.write("Scraping completed.")
```

---

### Handling IP Bans and CAPTCHAs with Bright Data

1. [Sign Up for Bright Data](https://brightdata.com/).
2. Set up the Bright Data scraping browser and integrate it into `scrape.py`.

---

### Parsing and Cleaning HTML Content

1. Update `scrape.py` with parsing functions:

```python
from bs4 import BeautifulSoup

def extract_body_content(html_content):
    soup = BeautifulSoup(html_content, "html.parser")
    return str(soup.body)

def clean_body_content(body_content):
    soup = BeautifulSoup(body_content, "html.parser")
    for script_or_style in soup(["script", "style"]):
        script_or_style.extract()
    cleaned_content = soup.get_text(separator="\n")
    return "\n".join([line.strip() for line in cleaned_content.splitlines() if line.strip()])
```

2. Update `main.py` to display parsed content:

```python
if st.button("Scrape Site"):
    html_content = scrape_website(url)
    body_content = extract_body_content(html_content)
    cleaned_content = clean_body_content(body_content)
    st.text_area("Cleaned Content", cleaned_content, height=300)
```

---

### Integrating with LLaMA via LangChain

1. Install LLaMA and [[LangChain]].
2. Create `parse.py` to analyze scraped data using LLaMA:

```python
from langchain import Llama

def parse_with_llama(dom_chunks, parse_description):
    model = Llama(model_name="Llama-3.1")
    prompt_template = "Your description: {parse_description}\nContent: {dom_content}"
    parsed_results = []
    for chunk in dom_chunks:
        response = model.invoke(dom_content=chunk, parse_description=parse_description)
        parsed_results.append(response)
    return "\n".join(parsed_results)
```

3. Update `main.py` for AI analysis:

```python
parse_description = st.text_input("Describe what you want to parse:")

if st.button("Parse Content"):
    dom_chunks = split_dom_content(st.session_state.dom_content)
    result = parse_with_llama(dom_chunks, parse_description)
    st.write(result)
```

---

### Conclusion and Next Steps

You've built an AI-powered web scraper! Consider adding features like asynchronous processing, database integration, and user authentication.

**Resources:**

- Streamlit Documentation
- Selenium Documentation
- [Bright Data](https://brightdata.com/)
- BeautifulSoup Docs
- [LangChain Docs](https://langchain.com/)
- [LLaMA GitHub](https://github.com/facebookresearch/llama)

 [[Python]]