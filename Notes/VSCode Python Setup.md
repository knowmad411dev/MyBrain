---
tags:
- python
- vscode
- editors
---
## **VSCode Python Setup

Setting up [[VSCode]] [[Python]] programs

1. pip install pillow
2. python.exe -m pip install --upgrade pip
3.  pip install OpenAI
4.  pip install language-tool-python
5.   pip install scikit-learn
6.  pip install PyPDF2 openai tqdm langdetect wordcloud matplotlib
7.  pip install pdf2image markdownify pytesseract PyPDF2 pillow
	   pytesseract requires the Tesseract OCR software to be installed on your system.
	   Download it from Tesseract GitHub and add its installation path to your system PATH,
	   or specify the path in your code like this:
	   pytesseract.pytesseract.tesseract_cmd = r'path\to\tesseract.exe'
8.   pip install sumy nltk
9.  pip install playwright
	   playwright install
10.  pip install networkx

ok, that is all the pip installs. I did this in vscode terminal.

Here's what each of the commands you listed does:

### 1. `pip install pillow`

- **Pillow**: A popular Python Imaging Library (PIL) fork that allows you to manipulate and process images (e.g., open, save, edit).

### 2. `python.exe -m pip install --upgrade pip`

- Upgrades **pip**, the Python package installer, to the latest version using the `-m` module flag.

### 3. `pip install OpenAI`

- **OpenAI**: Installs the OpenAI Python client library, which provides tools for interacting with OpenAI's GPT models and other APIs.

### 4. `pip install language-tool-python`

- **Language-Tool-Python**: A wrapper for **LanguageTool**, which is a grammar, style, and spell-checking tool.

### 5. `pip install scikit-learn`

- **Scikit-Learn**: A machine learning library for Python that provides simple and efficient tools for data analysis, modeling, and machine learning algorithms.

### 6. `pip install PyPDF2 openai tqdm langdetect wordcloud matplotlib`

- Installs multiple packages:
    - **PyPDF2**: For working with PDF files (reading, writing, and modifying).
    - **OpenAI**: The OpenAI client library.
    - **tqdm**: A package that provides progress bars for Python loops and data processing.
    - **langdetect**: A language detection library, useful for detecting the language of a given text.
    - **wordcloud**: Generates word clouds from text data, useful for visualizing text frequency.
    - **matplotlib**: A popular library for creating static, animated, and interactive visualizations in Python.

### 7. `pip install pdf2image markdownify pytesseract PyPDF2 pillow`

- Installs multiple packages:
    - **pdf2image**: Converts PDF files to images using Poppler.
    - **markdownify**: Converts HTML content into Markdown format.
    - **pytesseract**: A wrapper for Google's **Tesseract-OCR**, used for extracting text from images.
    - **PyPDF2**: Library for manipulating PDF files.
    - **pillow**: Python Imaging Library for working with images.
- Note:
    - **Tesseract-OCR** needs to be installed separately on your system, and its path must be added to the system PATH or set in your code using `pytesseract.pytesseract.tesseract_cmd`.

### 8. `pip install sumy nltk`

- Installs two packages for natural language processing:
    - **sumy**: A library for automatic text summarization.
    - **nltk**: The **Natural Language Toolkit**, used for working with human language data, offering text processing libraries and various corpora.

### 9. `pip install playwright`

- **Playwright**: A web automation library used for headless browser automation (like Selenium).
- `playwright install`: Downloads browser binaries (e.g., Chromium, Firefox, WebKit) necessary to use Playwright.

### 10. `pip install networkx`

- **NetworkX**: A library for creating, analyzing, and manipulating complex networks and graphs. It is useful for network analysis tasks, such as social network analysis, graph-based data structure analysis, etc.

[[Python]]  [[VSCode]]