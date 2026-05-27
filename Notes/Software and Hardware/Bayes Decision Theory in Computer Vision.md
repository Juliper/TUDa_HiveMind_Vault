---
title: Bayes Decision Theory in Computer Vision
aliases:
  - Bayes Entscheidungstheorie
  - Naive Bayes Classifier
tags:
  - visual-computing
  - computer-vision
  - classification
description: "Probabilistic framework for classifying visual data using prior knowledge and observed features"
draft: false
---

> [!NOTE] Definition
> Bayes Decision Theory provides a probabilistic framework for classification by combining prior probabilities with observed evidence to compute the most likely class.

## Components

### A Priori Probability

The initial probability of a class before observing features:

$$P(C_k) \quad \text{where} \quad \sum_k P(C_k) = 1$$

### Conditional Probability (Likelihood)

The probability of observing features $x$ given class $C_k$:

$$p(x|C_k)$$

### A Posteriori Probability

The probability of class $C_k$ given observed features $x$:

$$p(C_k|x) = \frac{p(x|C_k) \cdot P(C_k)}{P(x)} = \frac{p(x|C_k) \cdot P(C_k)}{\sum_j p(x|C_j) \cdot P(C_j)}$$

$$\text{Posterior} = \frac{\text{Likelihood} \cdot \text{Prior}}{\text{Normalization factor}}$$

## Naive Bayes (Multidimensional)

For multiple independent features $x_1, \ldots, x_d$:

$$p(C_k|x_1, \ldots, x_d) = \prod_{i=1}^{d} \frac{p(x_i|C_k)}{P(x_i)} \cdot P(C_k)$$

> [!IMPORTANT]
> The Naive Bayes classifier assumes feature independence. This assumption is often violated in practice, but the classifier still produces good results despite this.

## Decision Rule

Classify as $C_1$ if $P(C_1|x) > P(C_2|x)$, which is equivalent to:

$$p(x|C_1) \cdot P(C_1) > p(x|C_2) \cdot P(C_2)$$

## Related Concepts

- [[Face Detection]]: a key application of Bayesian classification
- [[Pinhole Camera Model]]: the image formation model providing input data
