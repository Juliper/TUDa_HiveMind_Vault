---
title: Distance Metrics in Machine Learning
aliases:
  - Similarity Measures
  - Ähnlichkeitsmaße
  - Abstandsmaße
tags:
  - machine-learning
  - data-mining
description: "Functions that quantify similarity or dissimilarity between data points in feature space"
draft: false
---

> [!NOTE] Definition
> Distance metrics (or similarity measures) are functions that quantify how similar or dissimilar two data points are. Similarity is inversely related to distance: the more similar two points are, the smaller their distance. Identical points have distance 0.

The choice of metric fundamentally affects the performance of algorithms like [[K-Nearest Neighbors]] - there is no universally "correct" metric.

## Metrics for Real-Valued Features

### Euclidean Distance

The most common distance metric for continuous features:

$$dist(\vec{x}, \vec{y}) = \sqrt{\sum_{i=1}^{n} (x_i - y_i)^2}$$

### Cosine Similarity

Measures the angle between two vectors, ignoring magnitude:

$$\cos(\vec{x}, \vec{y}) = \frac{\vec{x} \cdot \vec{y}}{|\vec{x}||\vec{y}|} = \frac{\sum_{i=1}^{n} x_i y_i}{\sqrt{\sum_{i=1}^{n} x_i^2} \cdot \sqrt{\sum_{i=1}^{n} y_i^2}}$$

## Metrics for Binary (0/1) Features

For instances with binary features, let $X$ be the set of positive features of instance A and $Y$ the set of positive features of instance B:

| Metric | Formula | Properties |
|--------|---------|------------|
| **Matching coefficient** | $\|X \cap Y\|$ | Raw overlap count |
| **Dice coefficient** | $\frac{2\|X \cap Y\|}{\|X\| + \|Y\|}$ | Normalized, penalizes size differences |
| **Jaccard coefficient** | $\frac{\|X \cap Y\|}{\|X \cup Y\|}$ | Normalized by union, ignores shared negatives |
| **Overlap coefficient** | $\frac{\|X \cap Y\|}{\min(\|X\|, \|Y\|)}$ | Robust to set size differences |
| **Cosine** | $\frac{\|X \cap Y\|}{\sqrt{\|X\| \cdot \|Y\|}}$ | Geometric mean normalization |

> [!IMPORTANT]
> The choice of metric depends on the data domain. Euclidean distance works well for dense, continuous features. Cosine similarity excels for text/sparse data where magnitude is irrelevant. Jaccard is preferred for binary or set-based features.

## Related Concepts

- [[K-Nearest Neighbors]]: relies on distance metrics to define neighborhoods
- [[Curse of Dimensionality]]: distance metrics become less meaningful in high dimensions
