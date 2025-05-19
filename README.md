# Semantic-Textual-Similarity-STS-project

This project tackles Semantic Textual Similarity on SemEval English datasets by building and comparing three models: a traditional ML system with handcrafted linguistic features, an embedding-based ML model, and a provided Siamese BiLSTM for sentence representations.

## Description

This project aims to measure the semantic equivalence between pairs of sentences using multiple approaches:

1. **Traditional ML with handcrafted features**

   * Sentence preprocessing (tokenization, lowercasing, stopword removal)
   * Individual features: WordNet metrics, word alignment scores, POS‐tag overlap, TF–IDF, n‑gram overlap
   * Training and evaluation of feature–model combinations (linear regression, random forests) on STS datasets

2. **Embedding-based ML model**

   * Distributional (co‑occurrence) and distributed (Word2Vec) word representations
   * Vector aggregation (cosine, Euclidean) with/without Word Mover’s Distance
   * Analysis of aggregation strategies: mean vs. sum vs. max

3. **Neural Siamese BiLSTM**

   * Provided architecture for sentence encoding
   * Hyperparameter search on embedding size, hidden dimension, number of LSTM layers
   * Evaluation using Pearson correlation and MSE

## Results

### Baseline (Jaccard overlap + linear regression)

* Dev set: Pearson = 0.66, MSE = 0.05
* Test set: Pearson = 0.60, MSE = 0.06 citeturn2file8

### Feature-based models on development set

| Model / Combination           |  Pearson |             MSE             |
| ----------------------------- | :------: | :-------------------------: |
| Linear (bi‑trigram + TF–IDF)  |   0.72   |            0.043            |
| Linear (+ WordNet)            |   0.73   |            0.041            |
| Linear (all features)         |   0.74   |            0.041            |
| Random Forest (all features)  |   0.74   |            0.043            |
| XGBoost (all features)        |   0.75   |            0.043            |
| Gradient Boost (all features) | **0.75** | **0.041** citeturn2file5 |

### Feature‐based best on test set (Gradient Boost, comb. 4)

* Pearson = 0.65 vs. baseline 0.67
* MSE = 0.054 vs. baseline 0.50 citeturn2file13

### Cosine‐based aggregation (no WMD)

* Best config (mean aggregation, no POS) achieved Pearson = 0.6646, MSE = 0.0517 citeturn2file0
* Sum aggregation nearly identical performance

### Siamese BiLSTM (dev set)

| Embedding dim | Hidden dim | LSTM layers |  MSE |  Pearson |
| ------------: | ---------: | ----------: | ---: | -------: |
|            70 |        150 |           1 | 0.23 |     0.47 |
|           100 |        150 |           1 | 0.23 | **0.51** |

Best performance obtained with embedding 100, hidden 150, layers 1 citeturn2file16

---

*All results obtained on standard SemEval English STS datasets.*
