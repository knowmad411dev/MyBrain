---
tags:
- gpt
- python
- web
---

## **ChatGPT API RSS Scrapping

Here is the code used in the video for scraping RSS feeds and interacting with the ChatGPT API:  Basic RSS Feed Parsing with Feedparser:

```python
import feedparser

# RSS feed URL
rss_feed_url = "https://www.gizmodo.com/rss"

# Parse the RSS feed
feed = feedparser.parse(rss_feed_url)

# Print the title and link of each article
for entry in feed.entries:
    print(f"Title: {entry.title}")
    print(f"Link: {entry.link}")
    print()
2. Parsing Multiple RSS Feeds and Combining Titles:
python
Copy code
import feedparser

# List of RSS feeds to parse
rss_feeds = [
    "https://www.gizmodo.com/rss",
    "https://www.engadget.com/rss.xml",
    "https://feeds.arstechnica.com/arstechnica/index"
]

# Empty list to store all titles
all_titles = []

# Parse each RSS feed and append titles to the list
for feed_url in rss_feeds:
    feed = feedparser.parse(feed_url)
    for entry in feed.entries:
        all_titles.append(entry.title)

# Print the total number of articles and their titles
print(f"Total Articles: {len(all_titles)}")
for title in all_titles:
    print(f"Title: {title}")
3. Using ChatGPT API to Process Titles:
python
Copy code
import openai

# Your OpenAI API key
openai.api_key = 'your-api-key-here'

# Function to send the titles to the ChatGPT API
def get_product_names_from_titles(titles):
    # Prepare the prompt for ChatGPT
    prompt = (
        "You are a database system. List all product names from the following titles:\n"
        + "\n".join(titles)
    )

    # Make a request to the GPT-4 model
    response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[
            {"role": "system", "content": "You are a database computer."},
            {"role": "user", "content": prompt},
        ],
        temperature=0,
        max_tokens=500
    )

    # Extract the response
    return response.choices[0].message['content']

# List of titles (as obtained from RSS feeds)
titles = [
    "Apple releases iPhone 15",
    "Google announces new Pixel phone",
    "Tesla introduces new Model X"
]

# Get product names from the titles using the ChatGPT API
product_names = get_product_names_from_titles(titles)
print(product_names)
4. Scraping Full Articles with BeautifulSoup:
python
Copy code
import requests
from bs4 import BeautifulSoup

# URL of the article to scrape
url = "https://www.arstechnica.com/some-article"

# Send a GET request to the URL
response = requests.get(url)

# Parse the HTML content with BeautifulSoup
soup = BeautifulSoup(response.text, "html.parser")

# Extract all the text within <p> tags (paragraphs)
article_text = " ".join([p.get_text() for p in soup.find_all('p')])

# Print the article text
print(article_text)
5. Summarizing and Tagging Articles with ChatGPT:
python
Copy code
import openai

# Function to summarize an article and create tags using ChatGPT API
def summarize_and_tag_article(article_text):
    # Create the request for a summary
    summary_response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=[
            {"role": "system", "content": "You are a journalist."},
            {"role": "user", "content": f"Summarize this article in 25 words:\n{article_text}"}
        ],
        temperature=0,
        max_tokens=50
    )

    # Create the request for tags
    tags_response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=[
            {"role": "system", "content": "You are a journalist."},
            {"role": "user", "content": f"Provide 5 tags for this article:\n{article_text}"}
        ],
        temperature=0,
        max_tokens=20
    )

    # Extract and return the summary and tags
    summary = summary_response.choices[0].message['content']
    tags = tags_response.choices[0].message['content']
    return summary, tags

# Sample article text (as obtained from scraping)
article_text = "Apple has announced the iPhone 15, which comes with a range of new features including an improved camera and faster processor."

# Get the summary and tags from the article text using ChatGPT
summary, tags = summarize_and_tag_article(article_text)

print("Summary:", summary)
print("Tags:", tags)
```

[[Web Scrapping]]  [[Python]]  [[ChatGPT]]