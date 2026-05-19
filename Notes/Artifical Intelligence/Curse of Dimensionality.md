---
title: Curse of Dimensionality
aliases:
  - Fluch der hohen Dimensionen
  - High-Dimensional Curse
tags:
  - machine-learning
  - data-mining
description: "The phenomenon where data becomes exponentially sparser as the number of dimensions increases, degrading ML algorithm performance"
draft: false
---

> [!NOTE] Definition
> The curse of dimensionality describes the phenomenon where the number of training examples needed to maintain a given data density grows **exponentially** with the number of dimensions (features). In high-dimensional spaces, data points become sparse, distances become less meaningful, and algorithms like [[K-Nearest Neighbors]] degrade.

## How It Works

The data density is proportional to $N^{1/d}$, where $N$ is the number of samples and $d$ is the dimensionality.

To cover a fraction $r$ of the volume in a $d$-dimensional unit hypercube, the side length of the required subcube is $r^{1/d}$. This means:

| Dimensions $d$ | Samples needed for same density as 100 in 1D |
|:-:|:-:|
| 1 | $100^{1/1} = 100$ |
| 2 | $100^{2/1} = 10{,}000$ |
| 10 | $100^{10} = 10^{20}$ |

> [!IMPORTANT]
> At $d = 10$, capturing just 10% of the data in a neighborhood requires covering 80% of the range of each feature. The "nearest neighbors" are no longer meaningfully close.

## Impact on kNN

For [[K-Nearest Neighbors]], this means:
- Neighborhoods become extremely sparse
- The concept of "nearest" loses its meaning since all points are roughly equidistant
- The [[Bias-Variance Tradeoff]] tilts toward high variance

## General Rule of Thumb

As the number of features (dimensions) increases, the number of required training examples grows **exponentially** to maintain accurate predictions. This applies to all machine learning algorithms, not just kNN.

## Mitigation Strategies

- **Feature selection**: remove irrelevant dimensions
- **Dimensionality reduction**: PCA, t-SNE, autoencoders
- **Regularization**: constrain model complexity
- Use algorithms less sensitive to dimensionality (e.g., [[Linear Regression]] with regularization)

## Related Concepts

- [[K-Nearest Neighbors]]: most directly affected by the curse
- [[Bias-Variance Tradeoff]]: high dimensions increase variance
- [[Overfitting]]: more dimensions make overfitting more likely
- [[Linear Regression]]: model complexity grows linearly with $p$ (number of features)
