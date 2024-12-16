---
tags:
- learning
- math
- machine-learning
video-url: https://www.youtube.com/watch?v=BT6Aw6Q75Yg&list=WL&index=2
---

## **All Learning Algorithms Explained

**Machine Learning Algorithms: Comprehensive Overview**

Machine learning involves various algorithms that can be categorized based on their purposes, such as classification, regression, clustering, or dimension reduction. Below, we provide an overview of some key machine learning algorithms, including definitions, instructions, and applicable formulas. This overview aims to demystify the fundamental concepts and applications of these algorithms.

### 1. **Linear Regression**

- **Definition**: Linear Regression is a **supervised learning algorithm** used to model the relationship between a continuous target variable (dependent) and one or more independent variables (features).
- **Application**: Used for predicting continuous values, such as house prices, temperature, or sales forecasts.
- **Formula**: The model fits a **linear equation** of the form:

  ‘y = a + b*x’,

  where **y** is the dependent variable, **x** represents independent variables, and **a** and **b** are coefficients determined by minimizing the sum of squared distances between the actual data points and the predicted regression line.

### 2. **Support Vector Machine (SVM)**

- **Definition**: SVM is a **supervised learning algorithm** used for classification and regression tasks.
- **Application**: Primarily for **classification**; useful for cases where the number of features is greater than the number of samples.
- **Decision Boundary**: SVM draws a decision boundary (hyperplane) to separate data into classes. The goal is to **maximize the margin** between support vectors (data points closest to the hyperplane).
- **Formulas**: The optimization problem is to minimize ‘||w||^2’ while ensuring that each data point is classified correctly (using constraints like ‘w ⋅ x_i + b ≥ 1 for yi=1’).

### 3. **Naïve Bayes Classifier**

- **Definition**: A **supervised learning algorithm** used for classification. It is based on **Bayes' theorem** and assumes **feature independence**.
- **Application**: Text classification, spam detection, and sentiment analysis.
- **Bayes' Theorem**: Given as:

  ‘P(A|B) = (P(B|A) * P(A)) / P(B)’,

  where **P(A|B)** is the posterior probability, **P(B|A)** is the likelihood, **P(A)** is the prior probability, and **P(B)** is the evidence. The classifier uses this theorem to calculate the probability of a class given a set of features.

### 4. **Logistic Regression**

- **Definition**: A **supervised learning algorithm** for **binary classification** tasks.
- **Application**: Useful for problems like email spam detection and customer churn prediction.
- **Sigmoid Function**: Logistic regression uses the **sigmoid (logistic) function**:

  ‘f(x) = 1 / (1 + e^{-z})’,

  where **z** is the output of the linear combination of input features. This function maps the output to a value between 0 and 1.

- **Classification Rule**: If the output is greater than 0.5, it predicts class **1**, otherwise class **0**.

### 5. **K-Nearest Neighbors (KNN)**

- **Definition**: KNN is a **supervised learning algorithm** used for both **classification and regression**.
- **Application**: Predicting labels by looking at **neighboring points** in the dataset.
- **Working**: The predicted value or label is determined by the **majority class** or the **mean** of **k closest points**. Choosing an optimal **K value** is crucial—too low results in overfitting, while too high leads to underfitting.

### 6. **Decision Tree**

- **Definition**: A **supervised learning algorithm** that splits the data based on features to create a **tree structure** of decisions.
- **Application**: Works well for **classification** and **regression** tasks.
- **Tree Construction**: The tree asks **questions at each node**, splitting based on the feature that most effectively separates classes or reduces variance (e.g., maximizing **information gain** or minimizing **impurity**).
- **Overfitting Risk**: Decision trees can **overfit** if they grow too deep, as they end up being highly specific to training data.

### 7. **Random Forest**

- **Definition**: Random Forest is an **ensemble** algorithm consisting of multiple **decision trees**.
- **Application**: Used for both **classification** and **regression**.
- **Bagging**: Random Forest uses a technique called **bagging** that trains multiple trees on **bootstrapped samples** of the data and **aggregates** the predictions (either **mean** or **majority voting**).
- **Pros**: It reduces overfitting seen in single decision trees and performs well on various datasets.

### 8. **Gradient Boosted Decision Trees (GBDT)**

- **Definition**: GBDT is another **ensemble method** that uses **boosting**, combining decision trees sequentially.
- **Application**: Suitable for both **classification** and **regression**, providing a **more accurate model** compared to Random Forest.
- **Boosting**: Trees are added sequentially to correct the errors of previous trees. Unlike bagging, boosting focuses on **weighted data** and attempts to reduce errors iteratively.

### 9. **K-Means Clustering**

- **Definition**: An **unsupervised learning algorithm** that partitions data into **K clusters** based on **similarities**.
- **Application**: Useful for grouping data where labels are not available.
- **Working**:
  1. Randomly assign **K centroids**.
  2. Assign each data point to the **nearest centroid**.
  3. Update centroids by calculating the **mean** of each cluster.
  4. Repeat until convergence.
- **Challenge**: The number of clusters **K** must be predetermined.

### 10. **DBSCAN (Density-Based Spatial Clustering of Applications with Noise)**

- **Definition**: A **density-based clustering** algorithm that can find **arbitrary-shaped clusters** and identify **outliers**.
- **Application**: Suitable for **spatial clustering** and situations involving **noisy data**.
- **Parameters**:
  - **EPS**: The maximum distance to consider a point a neighbor.
  - **MinPts**: Minimum number of points to form a cluster.
- **Point Classification**: Points are labeled as **core points**, **border points**, or **outliers**.

### 11. **Principal Component Analysis (PCA)**

- **Definition**: **Dimensionality reduction** algorithm used to transform features into a lower-dimensional space while preserving **maximum variance**.
- **Application**: Often used as a **pre-processing** step for other algorithms, especially when data has many features.
- **Components**: **Principal Components** are new features that represent the original data in a reduced form, ranked by the amount of **variance explained**.

### Summary Table of Use-Cases:

| Algorithm                 | Type               | Use-Case                           | Key Strengths                     |
|---------------------------|--------------------|------------------------------------|-----------------------------------|
| Linear Regression         | Supervised         | Predicting continuous values       | Simplicity, explainability        |
| SVM                       | Supervised         | Classification                     | Works well for high-dimension data|
| Naïve Bayes              | Supervised         | Text classification                | Speed, simplicity                 |
| Logistic Regression       | Supervised         | Binary classification              | Effective for simple tasks        |
| K-Nearest Neighbors (KNN) | Supervised         | Both classification & regression   | Non-parametric, simple to implement|
| Decision Tree             | Supervised         | Predictive modeling                | Easy to interpret                 |
| Random Forest             | Ensemble           | Improve Decision Tree performance  | Reduces overfitting               |
| GBDT                      | Ensemble           | Boosted performance on small data  | Highly accurate predictions       |
| K-Means Clustering        | Unsupervised       | Grouping unlabelled data           | Fast, intuitive                   |
| DBSCAN                    | Unsupervised       | Outlier detection                  | Works with arbitrary cluster shapes|
| PCA                       | Unsupervised       | Dimensionality reduction           | Handles multi-dimensional data    |

This overview covers the key machine learning algorithms, outlining their definitions, applications, strengths, and relevant formulas. Each algorithm has a unique application scope, and the choice depends on the specific characteristics of the dataset and the problem to solve. Understanding the differences in their use-cases helps in choosing the optimal algorithm for predictive modeling, clustering, and data interpretation tasks.

[[Math]]  [[Learning]]  [[Machine learning]]