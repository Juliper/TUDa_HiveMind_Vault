---
title: ROC Curve
aliases:
  - Receiver Operating Characteristic
  - ROC Analysis
  - AUC
  - Area Under the Curve
tags:
  - machine-learning
  - model-evaluation
  - classification
description: "A plot of true positive rate vs false positive rate across all decision thresholds, used to evaluate classifier quality independently of a specific threshold"
draft: false
---

> [!NOTE] Definition
> A ROC (Receiver Operating Characteristic) curve visualizes classifier performance by plotting the True Positive Rate (TPR) against the False Positive Rate (FPR) for every possible decision threshold $\theta$. It evaluates the **decision function** rather than a specific classifier configuration.

## Why ROC Analysis?

Accuracy alone can be misleading, especially with imbalanced classes. If $P(+1) = 3\%$, a 5% error rate is actually poor. ROC analysis evaluates the decision function $f(\mathbf{x})$ independently of any specific threshold.

## How to Read a ROC Curve

| Curve Shape | Meaning |
|---|---|
| Top-left corner $(0, 1)$ | Perfect classifier |
| Diagonal line | Random guessing |
| Above diagonal | Better than random |
| Below diagonal | Worse than random (invert predictions) |

The threshold $\theta$ controls the tradeoff:
- **High $\theta$**: fewer false positives but more false negatives
- **Low $\theta$**: fewer false negatives but more false positives

## Constructing a ROC Curve

1. Sort all test instances by their score $f(\mathbf{x})$ in descending order
2. Initialize $TP = 0$, $FP = 0$
3. For each instance in the sorted list:
   - If positive: increment $TP$
   - If negative: increment $FP$
   - Plot point at $(\frac{FP}{N}, \frac{TP}{P})$

Each point on the curve corresponds to a specific threshold value.

## Area Under the Curve (AUC)

The AUC summarizes the entire ROC curve in a single number:

$$AUC = P(f(x_+) > f(x_-))$$

where $x_+$ is a random positive instance and $x_-$ is a random negative instance.

| AUC Value | Interpretation |
|---|---|
| 1.0 | Perfect classifier |
| 0.5 | Random guessing |
| < 0.5 | Worse than random |

AUC is computed by summing the trapezoid areas under the curve.

> [!IMPORTANT]
> AUC measures the probability that the classifier ranks a random positive instance higher than a random negative instance. It is threshold-independent and works well for comparing classifiers.

## Related Concepts

- [[Confusion Matrix]]: each point on the ROC curve corresponds to a specific confusion matrix
- [[Precision and Recall]]: alternative evaluation focusing on the positive class
- [[Logistic Regression]]: produces a decision function whose ROC can be analyzed
