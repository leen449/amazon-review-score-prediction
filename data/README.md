## Overview

The dataset used in this project is the **Amazon Fine Food Reviews** dataset, which contains customer reviews for food products sold on Amazon. The dataset includes:
- Review text
- Summary information
- Rating scores
- Metadata related to each review

Due to GitHub file size limitations, the dataset is not stored in this repository. Instead, users must download it manually and place it in the appropriate directory before running the project notebooks.

## Dataset Source

The dataset can be downloaded from Kaggle:

[Amazon Fine Food Reviews Dataset](https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews)

The dataset is originally compiled from Amazon product reviews and is commonly used for research in sentiment analysis and text classification.

# Generating the Cleaned Dataset

After placing the dataset in the correct location, run the data preprocessing notebook:

```plaintext
notebooks/01_data_cleaning_eda.ipynb
```

This notebook performs the following steps:

- Removal of duplicate reviews
- Handling of missing values
- Combination of Summary and Text fields
- Removal of HTML tags and special characters
- Text normalization (lowercasing, punctuation removal)
- Tokenization, stopword removal, and lemmatization
- Filtering reviews to include only those from 2010 onward

The processed dataset will then be saved automatically.
