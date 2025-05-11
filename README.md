# Project Report: Sentence Classification in PubMed 200k RCT Dataset

## Author
Inès Duflos  
L3 Informatique - 2024

## Introduction
This project focuses on classifying sentences within the PubMed 200k Randomized Controlled Trial (RCT) dataset. The goal is to compare the performance of a baseline model using bag-of-words with a model leveraging pre-trained biomedical word embeddings. The study aims to enhance text classification understanding in the biomedical domain and evaluate the efficacy of domain-specific embeddings.

## Methodology

### Dataset Creation
- Loaded and processed PubMed dataset files.
- Removed empty lines and trial ID numbers.
- Organized labels and texts into `train_df` and `test_df` data frames.

### Data Preprocessing
- Applied the `scispacy` tokenizer and lemmatizer to all texts.
- Stored preprocessed results in a new column named `preprocessed_text`.

### Baseline Model (Bag-of-Words)
- Performed TF-IDF vectorization on preprocessed texts.
- Evaluated three classification models:
  - Multinomial Naïve Bayes
  - Logistic Regression
  - Random Forest
- Generated confusion matrices for each model.

### Word Embeddings Model
- Initially used `word2vec-google-news-300` embeddings due to technical challenges.
- Later incorporated 200-dimensional biomedical word embeddings from [this source](https://github.com/piskvorky/gensim-data/issues/28).
- Vectorized tokens and applied Logistic Regression for classification.

## Results and Comparison

### Performance Metrics

| Model                           | Precision | Recall | F1 Score | Accuracy |
|---------------------------------|-----------|--------|----------|----------|
| **Baseline Models**             |           |        |          |          |
| Multinomial Naïve Bayes         | 0.522     | 0.522  | 0.522    | 0.68     |
| Logistic Regression             | 0.66      | 0.67   | 0.664    | 0.75     |
| Random Forest                   | 0.614     | 0.632  | 0.623    | 0.73     |
| **Word Embeddings Models**      |           |        |          |          |
| Pre-trained Biomedical Embeddings | 0.441    | 0.485  | 0.428    | 0.485    |
| Word2vec-google-news-300        | 0.475     | 0.501  | 0.449    | 0.501    |

### Key Findings
- **Baseline Models**: Logistic Regression outperformed others in precision, recall, F1-score, and accuracy. Multinomial Naïve Bayes had the lowest performance.
- **Word Embeddings Models**: Underperformed compared to baseline models. The `word2vec-google-news-300` model slightly outperformed biomedical embeddings but still fell short.
- **Confusion Matrices**: Revealed significant misclassifications for labels like `Background`, `Conclusions`, and `Objective`, often mislabeled as `Methods` or `Results` due to class imbalance.

## Discussion
- The baseline models, particularly Logistic Regression, were more effective for this dataset.
- The poor performance of word embeddings might stem from insufficient dimensionality or lack of fit for the dataset. A 400-dimensional biomedical embedding could have yielded better results but was impractical due to computational constraints.

## Conclusion
The most efficient model for this project was **Logistic Regression**. While word embeddings showed potential, their performance was suboptimal, possibly due to model selection or training limitations. Despite Logistic Regression's superior results, there remains room for improvement in classification accuracy.

---
