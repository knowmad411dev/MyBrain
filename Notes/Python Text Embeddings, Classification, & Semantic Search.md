---
github_link: https://github.com/ShawhinT/YouTube-Blog/tree/main/LLMs/text-embeddings
tags:
- python
- llm
video-url: https://www.youtube.com/watch?v=sNa_uiqSlJo&list=WL&index=67
---

## **Python Text Embeddings, Classification, & Semantic Search**

This video by Sha explores the potential of **text embeddings** and discusses two primary use cases: **text classification** and **semantic search**. Here's a detailed summary of the key concepts, step-by-step instructions, and relevant code snippets covered in the video.

### **Introduction to Text Embeddings**

- **Text embeddings** convert textual data into numerical vectors. These embeddings capture the inherent meaning of the text, unlike traditional keyword matching approaches.
- For example, job descriptions can be converted into vectors, and similar roles (e.g., "data analyst" and "data visualization specialist") will have embeddings located near each other in vector space, enabling tasks like **classification** and **semantic search**.

### **Why Use Text Embeddings Instead of LLMs (Large Language Models)?**

1. **Lower computational and financial cost** compared to LLMs like ChatGPT.
2. **Fewer security risks**, such as avoiding prompt injection or data leakage.
3. **Predictable results** due to the deterministic nature of embeddings, unlike LLMs that may produce unpredictable output.

While LLMs are effective for some tasks (e.g., summarization), embeddings provide a more controlled, scalable, and cost-effective solution for other AI needs.

---

### **Use Case 1: Text Classification**

**Text classification** involves assigning a label to a given text, such as determining whether a job description is related to a "data scientist" role.

#### **How It Works (Code Walkthrough)**

1. **Install Necessary Libraries**:

    ```python
    import openai
    import pandas as pd
    import numpy as np
    import matplotlib.pyplot as plt
    from sklearn.ensemble import RandomForestClassifier
    from sklearn.metrics import roc_auc_score
    ```

2. **Load the Dataset** (synthetic job descriptions from GitHub):

    ```python
    df_train = pd.read_csv('path_to_your_dataset.csv')
    ```

3. **Generate Embeddings**:

    - Use OpenAI API to convert text data into embeddings:

    ```python
    def generate_embeddings(text, api_key):
        response = openai.Embedding.create(input=text, model="text-embedding-ada-002", api_key=api_key)
        return response['data'][0]['embedding']
    
    df_train['embeddings'] = df_train['job_description'].apply(generate_embeddings, api_key="your_secret_key")
    ```

4. **Prepare Data for Training**:

    - Extract embeddings and labels into variables `X` and `y`:

    ```python
    X = np.vstack(df_train['embeddings'])
    y = df_train['is_data_scientist']  # True or False
    ```

5. **Train a Classifier**:

    - Use a Random Forest classifier to train the model:

    ```python
    clf = RandomForestClassifier()
    clf.fit(X, y)
    ```

6. **Evaluate the Model**:

    - Compute accuracy and ROC AUC scores:

    ```python
    y_pred = clf.predict(X)
    roc_score = roc_auc_score(y, y_pred)
    print(f"ROC AUC Score: {roc_score}")
    ```

The output from this classifier shows how effectively it identifies job descriptions as related to data scientists.

---

### **Use Case 2: Semantic Search**

**Semantic search** retrieves documents based on meaning rather than just keywords. For instance, a query like "I need someone to build my data infrastructure" can return resumes of "data engineers," even if those exact words aren't used.

#### **How It Works (Code Walkthrough)**

1. **Install Necessary Libraries**:

    ```python
    import pandas as pd
    import numpy as np
    from sentence_transformers import SentenceTransformer
    from sklearn.decomposition import PCA
    import matplotlib.pyplot as plt
    ```

2. **Load Data and Embeddings**:

    ```python
    df_resumes = pd.read_csv('path_to_resume_dataset.csv')
    model = SentenceTransformer('all-MiniLM-L6-v2')
    df_resumes['embeddings'] = df_resumes['job_description'].apply(model.encode)
    ```

3. **Dimensionality Reduction**:

    - Reduce the dimensionality using PCA for visualization:

    ```python
    pca = PCA(n_components=2)
    reduced_embeddings = pca.fit_transform(np.vstack(df_resumes['embeddings']))
    plt.scatter(reduced_embeddings[:, 0], reduced_embeddings[:, 1], c='roles')
    plt.show()
    ```

4. **Perform Semantic Search**:

    - Encode the user’s query and find the closest resumes:

    ```python
    query = "I need someone to build my data infrastructure"
    query_embedding = model.encode(query)
    
    distances = np.linalg.norm(np.vstack(df_resumes['embeddings']) - query_embedding, axis=1)
    closest_indices = np.argsort(distances)[:10]
    results = df_resumes.iloc[closest_indices]
    print(results['job_description'])
    ```

    This code returns the top 10 resumes that match the meaning of the user’s query.

---

### **Improving Semantic Search**

- **Hybrid Search**: Combine keyword search with semantic search for better results.
- **Ranker Models**: Use ranker models to rerank search results based on similarity scores.
- **Fine-Tuning Embeddings**: For specific domains (e.g., technical jargon), fine-tuning the embedding model can improve accuracy.

### **Final Thoughts**

- **Text embeddings** are a highly efficient, scalable way to perform tasks like classification and search. They are a great alternative when full-scale LLMs are either overkill or impractical due to cost or security concerns.
- More detailed examples and data are shared in the presenter's GitHub repository for hands-on implementation.

---

[[Python]]  [[LLM]]
