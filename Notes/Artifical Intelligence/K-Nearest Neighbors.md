---
title: K-Nearest Neighbors
aliases:
  - kNN
  - K-nächste-Nachbarn
  - k-Nearest Neighbors
tags:
  - machine-learning
  - classification
  - regression
description: "Instance-based learning algorithm that classifies or predicts by finding the k most similar training examples"
draft: false
---

> [!NOTE] Definition
> K-Nearest Neighbors (kNN) is a **local**, instance-based learning algorithm that makes predictions for a new data point $\vec{x}$ by finding the $k$ closest training examples (neighbors) in feature space and aggregating their labels or values.

kNN is a **lazy learner** - it stores all training data and only computes at prediction time. It contrasts with **global models** like [[Linear Regression]], which find a single separating hyperplane for all examples at once.

## How It Works

Each instance has the form $\langle \vec{x}_i, f(\vec{x}_i) \rangle$. For a new test instance $\vec{x}$:

1. Compute the distance between $\vec{x}$ and every training instance using a [[Distance Metrics in Machine Learning|distance metric]]
2. Select the $k$ nearest neighbors $n_1, \ldots, n_k$
3. Determine the prediction using a **selection function** $A$:

$$f(\vec{x}) = A(f(n_1), \ldots, f(n_k))$$

The neighborhood $N_k(\vec{x})$ is defined by the chosen distance metric. When neighborhoods don't overlap, there are at most $\frac{N}{k}$ neighborhoods.

## Selection Function (Auswahlfunktion)

The aggregation strategy depends on the task:

| Task | Method | Formula |
|------|--------|---------|
| **Classification** | Majority vote | Most frequent label among neighbors |
| **Regression** | Average | $f(x) = \frac{1}{k} \sum_{i=1}^{k} f(n_i)$ |
| **Weighted regression** | Similarity-weighted | $f(x) = \sum_{i=1}^{k} sim(n_i, x) \cdot f(n_i)$ |
| **Distance-weighted** | Inverse distance | $f(x) = \frac{\sum_{i=1}^{k} w_i \cdot f(n_i)}{\sum_{i=1}^{k} w_i}$ with $w_i = \frac{1}{d(n_i, x)^2}$ |

> [!IMPORTANT]
> The choice of $k$ critically affects performance. Small $k$ (e.g., $k=1$) leads to [[Overfitting]] - zero training error but high test error. Large $k$ produces smoother decision boundaries but may underfit.

## Asymptotic Properties

When $k/N \to 0$ and $k \to \infty$ (both $k$ and $N$ grow, but $k$ slower), the kNN prediction converges to the expected prediction. However, the [[Curse of Dimensionality]] limits this in practice - in high dimensions, neighborhoods become sparse and the "nearest" neighbors may not be meaningfully close.

## Example

For handwritten digit recognition (e.g., MNIST-style data):
- Each digit is a $12 \times 16$ matrix of grayscale values $\in [0, 1]$, flattened to a 192-dimensional vector
- With $k=1$ (nearest neighbor): recognition rate of 0.934
- With $k=3$ (majority vote): recognition rate of 0.945

## Related Concepts

- [[Distance Metrics in Machine Learning]]: defines how "closeness" is measured
- [[Overfitting]]: kNN with small $k$ is prone to overfitting
- [[Curse of Dimensionality]]: limits kNN effectiveness in high-dimensional spaces
- [[Bias-Variance Tradeoff]]: small $k$ means low bias but high variance
- [[Cross-Validation]]: used to find optimal $k$
