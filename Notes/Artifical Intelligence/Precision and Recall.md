---
title: Precision and Recall
aliases:
  - Precision
  - Recall
  - F-Measure
  - F1-Score
tags:
  - machine-learning
  - model-evaluation
  - classification
description: "Evaluation metrics from information retrieval that measure classifier quality on the positive class, with the F-measure combining both"
draft: false
---

> [!NOTE] Definition
> Precision measures the fraction of positive predictions that are actually positive, while recall measures the fraction of actual positives that are correctly predicted. Together they characterize classifier performance on the positive class, especially useful for imbalanced datasets.

## Definitions

$$\text{Precision} = \frac{TP}{TP + FP}$$

Precision answers: "Of everything predicted positive, how much is truly positive?"

$$\text{Recall} = \frac{TP}{TP + FN}$$

Recall answers: "Of everything that is truly positive, how much did we find?"

> [!IMPORTANT]
> Precision and recall originate from information retrieval. Recall is identical to the True Positive Rate (TPR) from the [[Confusion Matrix]].

## Precision-Recall Tradeoff

Precision and recall are inversely related as the decision threshold changes:
- **Higher threshold**: higher precision, lower recall (fewer but more confident predictions)
- **Lower threshold**: higher recall, lower precision (catch more positives but with more false alarms)

## F-Measure

The F-measure (F1-score) combines precision and recall into a single number using the harmonic mean:

$$F = \frac{2 \cdot \text{Precision} \cdot \text{Recall}}{\text{Precision} + \text{Recall}}$$

The harmonic mean penalizes extreme imbalances - if either precision or recall is very low, the F-measure will be low.

## Precision-Recall Breakeven Point (PRBEP)

The PRBEP is the threshold $\theta$ at which precision equals recall:

$$\text{Precision}(\theta) = \text{Recall}(\theta) = \text{PRBEP}$$

This provides a single-number summary of the precision-recall curve, similar to how [[ROC Curve|AUC]] summarizes the ROC curve.

## When to Use

| Metric | Best For |
|---|---|
| [[ROC Curve\|ROC/AUC]] | General classifier comparison, balanced or moderately imbalanced data |
| **Precision/Recall** | Highly imbalanced data, when positive class is more important |
| **F-Measure** | Single-number summary balancing precision and recall |

## Related Concepts

- [[Confusion Matrix]]: precision and recall are derived from TP, FP, FN
- [[ROC Curve]]: alternative evaluation using TPR vs FPR
- [[Logistic Regression]]: threshold selection directly affects precision-recall tradeoff
