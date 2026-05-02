## Amazon Fine Food Review Score Prediction
<img width="600" height="600" alt="image" src="https://github.com/user-attachments/assets/ba417280-e9ea-4390-b9d5-d8eca5a7a20b" />

# Overview


Online reviews contain valuable information about customer satisfaction and product quality. Automatically predicting review scores from textual feedback can help businesses analyze customer sentiment, detect dissatisfaction, and summarize large volumes of reviews efficiently.

This project aims to predict the **rating score (1–5 stars)** of Amazon Fine Food product reviews using natural language processing (NLP) and machine learning techniques using two different feature engineering techniques and three classification models.

The project follows a full machine learning workflow including **data preprocessing, exploratory data analysis (EDA), feature engineering, model training, hyperparameter tuning, and performance evaluation**.

* * *

# Task Definition

**Problem Type:**  
Multi-class text classification

**Input:**  
Review text created by combining the _Summary_ and _Text_ fields from the dataset.

**Output:**  
Predicted rating score from **1 to 5 stars**.

The objective is to learn patterns from the review text that correspond to different rating scores.

* * *

# Dataset

The project uses the **Amazon Fine Food Reviews dataset**, which contains customer reviews of food products sold on Amazon.

Each review includes several attributes such as:

-   Product ID
    
-   User ID
    
-   Review summary
    
-   Full review text
    
-   Rating score (1–5)
    
-   Review timestamp
    

### Dataset Characteristics

-   Reviews collected between **1999 and 2012**
    
-   Rating scale from **1 (very negative) to 5 (very positive)**
    
-   Textual reviews vary in length and writing style
    
-   Strong **class imbalance**, with the majority of reviews being 5-star ratings
    

### Data Preparation

To improve data quality and focus on more recent reviews, the following preprocessing steps were applied:

-   Removal of duplicate reviews
    
-   Handling missing values in the Summary field
    
-   Combining **Summary** and **Text** into a single review text
    
-   Removal of HTML tags
    
-   Lowercasing and normalization
    
-   Removal of punctuation and special characters
    
-   Tokenization and stopword removal
    
-   **Lemmatization** to reduce words to their base form
    
-   Removal of non-English reviews
    
-   Filtering reviews to include only those from **2010 onwards**
    

After preprocessing, the dataset is split into:

-   **70% Training set**
    
-   **10% Validation set**
    
-   **20% Test set**
    

To address class imbalance, the **training set was balanced by sampling an equal number of examples from each rating class which is 15000**, while the validation and test sets retained their original class distribution.

* * *

# Methods

Two feature engineering techniques and three models are used in this project.

## Feature Engineering

### TF-IDF with N-grams

Term Frequency–Inverse Document Frequency (TF-IDF) converts text into numerical vectors representing word importance.  
We use **n-grams (unigrams and bigrams)** to capture short phrases that convey sentiment.

### Average Word2Vec Embeddings

Word2Vec generates dense vector representations for words based on their context.  
Each review is represented by the **average of its word vectors**, creating a fixed-length embedding for the entire text.

* * *

## Machine Learning Models

### Logistic Regression (LR)

A linear classification model widely used for text classification problems.  
It is efficient, interpretable, and performs well with high-dimensional feature spaces such as TF-IDF.

### Linear Support Vector Machine (LSVM)

A support vector machine using a linear kernel.  
LSVM is known to perform strongly on text classification tasks due to its ability to handle sparse high-dimensional feature vectors.

### BERT (Bidirectional Encoder Representations from Transformers)
In addition to classical machine learning models, we implemented BERT, a transformer-based deep learning model that achieves state-of-the-art performance in many NLP tasks.
BERT captures contextual relationships between words by processing text bidirectionally, allowing it to better understand sentence meaning compared to traditional methods.
In this project, we fine-tuned the pre-trained **bert-base-cased** model for multi-class classification to predict review scores from the combined review text.
The model was trained for **3 epochs** with a learning rate of **0.00001**, following standard fine-tuning practices. The training set was balanced, while validation and test sets retained the original class distribution.

* * *

## Experiments

The following combinations are evaluated:

| Feature Representation | Model |
| --- | --- |
| TF-IDF | Logistic Regression |
| TF-IDF | Linear SVM |
| Word2Vec | Logistic Regression |
| Word2Vec | Linear SVM |
| Raw Text | BERT |

Hyperparameter tuning is performed using the **validation set**.

* * *

# Evaluation Metrics

Model performance is evaluated using several classification metrics.

### Macro F1 Score

The primary evaluation metric.  
Macro F1 treats all classes equally and is suitable for imbalanced datasets.

### Weighted F1 Score

Accounts for class imbalance by weighting classes according to their frequency.

### Accuracy

Measures the proportion of correct predictions.

### Precision and Recall

Evaluated per class to understand how well the model detects different rating levels.

### Confusion Matrix

Visualizes classification errors and shows which rating classes are commonly confused.

Final model performance is reported on the **test set**, which is not used during training or hyperparameter tuning.

* * *

# Final Results


| Model | Feature Representation | Macro F1 | Weighted F1 | Accuracy |
|------|----------------------|----------|-------------|----------|
| Logistic Regression | TF-IDF | 0.59 | 0.70 | 0.68 |
| Linear SVM | TF-IDF | 0.59 | 0.71 | 0.69 |
| Logistic Regression | Word2Vec | 0.46 | 0.62 | 0.59 |
| Linear SVM | Word2Vec | 0.46 | 0.65 | 0.63 |
| **BERT** | Raw Text | **0.67** | **0.77** | **0.75** |

* * *
## Results Analysis

The BERT model significantly outperformed traditional machine learning models across all evaluation metrics. This demonstrates the advantage of contextual embeddings over classical feature engineering methods such as TF-IDF and Word2Vec.

However, performance varies across classes. The model achieves strong results on the majority class (5-star reviews), while performance is lower on intermediate classes (2–4 stars). This is mainly due to the inherent class imbalance and the subjective nature of rating distinctions.

The confusion matrix shows that most errors occur between adjacent classes (e.g., 4 vs 5), indicating that the model captures general sentiment well but struggles with fine-grained distinctions.
* * *

# Repository Structure

    amazon-review-score-prediction/
    │
    ├── README.md
    ├── requirements.txt
    ├── .gitignore
    │
    ├── data/
    │   └── README.md
    │
    ├── notebooks/
    │   ├── 01_data_cleaning_eda/
    │   ├── 02_feature_engineering/
    │   └── 03_model_training/
    │
    ├── models/
    │   ├── lrtfidf__model.pkl
    │   ├── lsvm_tfidf_model.pkl
    │   └── tfidf_vectorizer.pkl
    ├── reports/
    │   ├── figures/
    │   └── results_table/
    │
    ├── docs/
    │   ├── proposal.pdf
    │   └── checkpoint_presentation.pdf
    │
    └── AUTHORS.md
    

* * *
