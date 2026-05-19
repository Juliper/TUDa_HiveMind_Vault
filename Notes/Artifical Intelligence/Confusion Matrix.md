---
title: Confusion Matrix
aliases:
  - Konfusionsmatrix
  - Error Matrix
tags:
  - machine-learning
  - model-evaluation
  - classification
description: "A table summarizing classifier performance by comparing predicted vs actual class labels across all test instances"
draft: false
---

> [!NOTE] Definition
> A confusion matrix is a table that visualizes the performance of a classifier by showing how often each true class was classified as each predicted class. It is the foundation for nearly all classification evaluation metrics.

## Binary Classification

| | Classified as + | Classified as - | |
|---|---|---|---|
| **Is +** | True Positives (TP) | False Negatives (FN) | $P = TP + FN$ |
| **Is -** | False Positives (FP) | True Negatives (TN) | $N = FP + TN$ |
| | $TP + FP$ | $FN + TN$ | $|E| = P + N$ |

## Evaluation Metrics

All standard metrics can be derived from the confusion matrix:

| Metric | Formula | Meaning |
|---|---|---|
| **True Positive Rate (TPR)** | $\frac{TP}{TP + FN}$ | Fraction of positives correctly classified |
| **False Positive Rate (FPR)** | $\frac{FP}{FP + TN}$ | Fraction of negatives incorrectly classified |
| **False Negative Rate (FNR)** | $\frac{FN}{TP + FN} = 1 - TPR$ | Fraction of positives missed |
| **True Negative Rate (TNR)** | $\frac{TN}{FP + TN} = 1 - FPR$ | Fraction of negatives correctly classified |
| **Accuracy** | $\frac{TP + TN}{N + P}$ | Fraction of all instances correctly classified |
| **Error Rate** | $\frac{FP + FN}{N + P}$ | Fraction of all instances misclassified |

> [!WARNING]
> Accuracy can be misleading with imbalanced classes. If 97% of instances are negative, a classifier that always predicts negative achieves 97% accuracy. Use [[Precision and Recall]] or [[ROC Curve|ROC analysis]] instead.

## Multi-Class Extension

For $K$ classes, the confusion matrix becomes a $K \times K$ table where entry $n_{ij}$ is the number of instances with true class $i$ classified as class $j$:

| | A | B | C | D | |
|---|---|---|---|---|---|
| **A** | $n_{AA}$ | $n_{BA}$ | $n_{CA}$ | $n_{DA}$ | $n_A$ |
| **B** | $n_{AB}$ | $n_{BB}$ | $n_{CB}$ | $n_{DB}$ | $n_B$ |
| **C** | $n_{AC}$ | $n_{BC}$ | $n_{CC}$ | $n_{DC}$ | $n_C$ |
| **D** | $n_{AD}$ | $n_{BD}$ | $n_{CD}$ | $n_{DD}$ | $n_D$ |

Accuracy is the sum of the diagonal divided by the total number of instances $|E|$.

## Related Concepts

- [[Precision and Recall]]: metrics derived from the confusion matrix for imbalanced data
- [[ROC Curve]]: evaluates classifiers across all decision thresholds
- [[Classification and Regression]]: confusion matrices apply to classification tasks
