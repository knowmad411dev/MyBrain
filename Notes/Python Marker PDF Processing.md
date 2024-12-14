---
Video-URL: https://www.youtube.com/watch?v=mdLBr9IMmgI&list=WL&index=2&t=301s
tags:
- python
- pdf
---

## **Python Marker PDF Processing**

This text discusses the challenges of converting PDF documents for use with Large Language Models (LLMs) and presents an open-source tool called **Marker** that effectively converts PDFs to Markdown format, making them more compatible with LLM applications.

### **Challenges of PDF Conversion for LLMs**

- **Complex Structure**: PDFs often contain various nested elements like text, images, tables, and different fonts, making data extraction difficult. The lack of a standard layout adds complexity.
- **Parsing Problems**: Converting PDFs to text accurately is challenging due to various fonts, encodings, and formatting. Techniques like Optical Character Recognition (OCR) are used but can be prone to errors.

### **Why Use Markdown for LLMs?**

- **Ease of Parsing**: Markdown is easier for LLMs to process, as it retains the structure and formatting of content (headers, images, tables).
- **Accurate Content Representation**: Markdown preserves the original layout and structure more effectively than plain text conversions.

### **Available Tools for PDF to Markdown Conversion**

- **Paid Options**:
    - **Mathpix**: A paid solution for converting PDFs to Markdown.
- **Open Source Options**:
    - **NuGet**: Developed by Meta, mainly focused on academic papers. Slower and less accurate compared to Marker.
    - **Marker**: A new open-source tool that outperforms NuGet by being faster and more accurate in extracting content from PDFs.

### **Comparative Performance of Marker vs. NuGet**

- **Speed**: Marker processes a single page in about 100 seconds, compared to 400 seconds by NuGet.
- **Accuracy**: Marker is nearly twice as accurate in retaining the structure and content of the original PDF.
- **Example Output**:
    - **NuGet's Output**: Misses the first few pages and the table of contents; confuses headers and footers with main content.
    - **Marker's Output**: Preserves the structure, including accurate extraction of the table of contents and chapters.

### **Features of Marker**

- **Document Support**: Optimized for books and scientific papers, but works well with other formats, such as resumes.
- **Language Support**: Claims to support "all languages," but the exact meaning is unclear.
- **Removes Unwanted Elements**: Cleans headers, footers, and artifacts from documents; formats tables, code blocks, and extracts images.
- **Equation Support**: Converts most equations to LaTeX format; complex equations might not convert perfectly.
- **Supports GPU/CPU/MPS**: Can run on various systems, including Apple Silicon.
- **Optional OCR Integration**: Uses the **Surya** package for OCR, created by the same author as Marker.

### **Limitations of Marker**

- **Incomplete LaTeX Conversion**: Not all equations convert perfectly.
- **Table Formatting Issues**: Tables are not always accurately formatted, requiring manual checking.
- **Whitespace and Line Span Issues**: Spaces and line spans might need manual correction.
- **Usage Restrictions**: Free for organizations under $5 million in gross revenue or lifetime VC funding in the last 12 months. Larger organizations require a license.

### **Installation and Setup**

1. **Create a New Conda Environment**:

    ```conda
    conda create --name marker python=3.9
    ```

    Activate the environment:

    ```conda
    conda activate marker
    ```

2. **Install PyTorch**: Select the appropriate installation command based on your operating system (Mac, Linux, or Windows).

    ```
    pip install torch torchvision torchaudio
    ```

3. **Install Marker**:

    ```
    pip install marker-pdf
    ```

    Optionally, install OCR support:

    ```
    pip install ocrmypdf
    ```

### **Usage Instructions**

- **Converting a Single PDF to Markdown**:

    ```
    marker_single --input path/to/pdf --output path/to/output/folder
    ```

    Optional parameters include `--batch_multiplier` to limit pages and `--language` for better OCR accuracy.

- **Output Structure**:
    - **Images**: Extracted separately and stored in an image folder.
    - **Metadata**: Saved in a JSON file detailing elements like page count, tables, equations, and language.
    - **Markdown File**: A structured Markdown file is created, with correct relative formatting, images, and references.

### **Testing Results with Marker**

Marker was tested on different document types, such as scientific papers and resumes. It was able to accurately extract images, text, and equations. The output closely resembles the original document in terms of structure and layout.

- **Issues Observed**: Some documents had images split into parts, requiring further manual adjustments.

### **Conclusion**

Marker is a promising open-source tool for converting complex PDFs into structured Markdown files, making them more suitable for LLM applications. While there are some limitations, its performance is commendable, and it significantly outperforms similar tools like NuGet.

[[Python]]