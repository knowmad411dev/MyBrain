---
tags:
- python
video-url: https://www.youtube.com/watch?v=HIvQWdqvl7o&list=WL&index=11
---
## **Python AI Projects

Here's a detailed overview of each of the five Python AI projects described in the text, including the instructions and example code. Each project gradually increases in difficulty, from basic sentiment analysis to a more complex AI agent.

### 1. Sentiment Analysis Tool

This project involves reading textual data and analyzing the sentiment, determining whether the content is positive, negative, or neutral. It is a great beginner project for learning natural language processing.

**Modules to Use:**
- **NLTK (Natural Language Toolkit)**: Provides a suite of text processing libraries, datasets, and other tools.
- **Pandas**: Useful for loading and preprocessing the text data.
- **Scikit-Learn (sklearn)**: For building and evaluating the machine learning model.

**Pip Installs Required:**
```bash
pip install nltk pandas scikit-learn
```

**Example Code:**
```python
import nltk
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.naive_bayes import MultinomialNB
from sklearn.metrics import accuracy_score

# Download data (e.g., movie reviews)
nltk.download('movie_reviews')

# Load dataset
reviews = pd.read_csv('movie_reviews.csv')  # Example dataset containing text reviews and labels

# Preprocess dataset
data = reviews[['text', 'label']]  # Selecting the required columns

# Vectorize textual data
vectorizer = CountVectorizer()
X = vectorizer.fit_transform(data['text'])
y = data['label']

# Split dataset into training and testing sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Train model
model = MultinomialNB()
model.fit(X_train, y_train)

# Evaluate model
y_pred = model.predict(X_test)
accuracy = accuracy_score(y_test, y_pred)
print(f'Accuracy: {accuracy * 100:.2f}%')

# Prediction function
def predict_sentiment(text):
    vector = vectorizer.transform([text])
    prediction = model.predict(vector)
    return 'Positive' if prediction == 1 else 'Negative'

# Test predictions
print(predict_sentiment("This movie was fantastic!"))
print(predict_sentiment("The movie was boring and too long."))
```

### 2. Image Classifier

This project involves building an image classifier using a dataset of images. You can use convolutional neural networks (CNNs) to classify images into various categories.

**Modules to Use:**
- **TensorFlow**: A framework for building deep learning models.
- **Keras**: A high-level API on top of TensorFlow to make the implementation easier.
- **Pandas, NumPy**: For handling and manipulating data.

**Pip Installs Required:**
```bash
pip install tensorflow matplotlib pandas numpy
```

**Example Code:**
```python
import tensorflow as tf
from tensorflow.keras import datasets, layers, models
import matplotlib.pyplot as plt

# Load dataset (CIFAR-10 example)
(X_train, y_train), (X_test, y_test) = datasets.cifar10.load_data()

# Normalize the dataset
X_train, X_test = X_train / 255.0, X_test / 255.0

# Create the model
model = models.Sequential([
    layers.Conv2D(32, (3,3), activation='relu', input_shape=(32, 32, 3)),
    layers.MaxPooling2D((2, 2)),
    layers.Conv2D(64, (3, 3), activation='relu'),
    layers.MaxPooling2D((2, 2)),
    layers.Flatten(),
    layers.Dense(64, activation='relu'),
    layers.Dense(10)  # 10 classes for CIFAR-10
])

# Compile and train the model
model.compile(optimizer='adam', loss='sparse_categorical_crossentropy', metrics=['accuracy'])
model.fit(X_train, y_train, epochs=10, validation_data=(X_test, y_test))

# Evaluate the model
test_loss, test_acc = model.evaluate(X_test, y_test)
print(f'Test accuracy: {test_acc * 100:.2f}%')

# Make a prediction
def classify_image(index):
    plt.imshow(X_test[index])
    plt.show()
    prediction = model.predict(X_test[index:index+1])
    print(f'Predicted label: {tf.argmax(prediction[0])}')

classify_image(0)
```

### 3. Voice Assistant with Speech Recognition

In this project, you create a voice assistant that takes spoken commands and performs actions, such as saving a note or accessing calendar events.

**Modules to Use:**
- **SpeechRecognition**: For converting speech to text.
- **Pyttsx3**: For text-to-speech.
- **Google API**: To integrate with Google Calendar.

**Pip Installs Required:**
```bash
pip install SpeechRecognition pyttsx3 google-api-python-client
```

**Example Code:**
```python
import speech_recognition as sr
import pyttsx3
from google.oauth2 import service_account
from googleapiclient.discovery import build

# Initialize recognizer and TTS engine
recognizer = sr.Recognizer()
engine = pyttsx3.init()

# Function to convert text to speech
def speak(text):
    engine.say(text)
    engine.runAndWait()

# Function to listen for user command
def listen():
    with sr.Microphone() as source:
        print("Listening...")
        audio = recognizer.listen(source)
    try:
        return recognizer.recognize_google(audio)
    except sr.UnknownValueError:
        return "Sorry, I did not understand that."

# Function to authenticate with Google Calendar
def authenticate_google():
    credentials = service_account.Credentials.from_service_account_file('credentials.json')
    service = build('calendar', 'v3', credentials=credentials)
    return service

# Access Google Calendar
def get_events(service):
    events = service.events().list(calendarId='primary', maxResults=10).execute()
    for event in events['items']:
        print(event['summary'])
        speak(event['summary'])

# Example usage
command = listen()
if "calendar" in command:
    service = authenticate_google()
    get_events(service)
elif "note" in command:
    note = listen()
    with open('notes.txt', 'a') as f:
        f.write(note + '\n')
    speak("Note saved.")
```

### 4. Recommendation System

This project involves building a recommendation system based on user preferences. You can use collaborative filtering techniques to recommend items such as movies or products.

**Modules to Use:**
- **Surprise**: For building recommendation models.
- **Pandas, NumPy**: For handling data.

**Pip Installs Required:**
```bash
pip install scikit-surprise pandas numpy
```

**Example Code:**
```python
from surprise import Dataset, Reader, SVD
from surprise.model_selection import train_test_split
from surprise import accuracy

# Load dataset
data = Dataset.load_builtin('ml-100k')  # MovieLens dataset

# Train-test split
trainset, testset = train_test_split(data, test_size=0.2)

# Use SVD for recommendations
model = SVD()
model.fit(trainset)

# Evaluate the model
predictions = model.test(testset)
accuracy.rmse(predictions)

# Recommend movies
def recommend_movies(user_id, num_recommendations=5):
    # Get all item ids
    movie_ids = data.raw_ratings[:, 1]
    predicted_ratings = [
        (movie_id, model.predict(user_id, movie_id).est) for movie_id in movie_ids
    ]
    predicted_ratings.sort(key=lambda x: x[1], reverse=True)
    return predicted_ratings[:num_recommendations]

print(recommend_movies(user_id=1))
```

### 5. AI Agent

The final project is an AI agent that can interact with its environment and respond to user queries by using natural language models (LLMs) and tools.

**Modules to Use:**
- **Langchain**: For managing conversational agents.
- **Llama Index**: For interacting with different LLMs.
- **OpenAI API or Llama**: For language models.

**Pip Installs Required:**
```bash
pip install langchain llama-index openai
```

**Example Code:**
```python
from langchain.agents import initialize_agent, Tool
from langchain.llms import OpenAI
from llama_index import Llama

# Create AI tools
def save_note_tool(note_text):
    with open('notes.txt', 'a') as file:
        file.write(note_text + '\n')
    return "Note saved successfully."

# Define Tools
note_tool = Tool(name="Note Tool", func=save_note_tool, description="Saves a note.")
tools = [note_tool]

# Create LLM and agent
llm = OpenAI(temperature=0.7)
agent = initialize_agent(tools=tools, llm=llm, verbose=True)

# Ask the agent to save a note
user_command = "Save a note: Remember to finish my AI project."
agent.run(user_command)
```

These projects are designed to help you gradually learn key AI and ML concepts. Feel free to customize these code snippets and explore each topic more deeply.

[[Python]]