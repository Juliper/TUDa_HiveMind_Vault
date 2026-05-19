---
title: Maximum Likelihood Estimation
aliases:
  - MLE
  - Maximum Likelihood
  - Likelihood-Maximierung
tags:
  - machine-learning
  - statistics
  - optimization
description: "A parameter estimation method that finds the parameters maximizing the probability of observing the given data"
draft: false
---

> [!NOTE] Definition
> Maximum Likelihood Estimation (MLE) is a method for estimating the parameters $\theta$ of a statistical model by finding the values that maximize the likelihood - the probability of the observed data given those parameters.

## How It Works

Given a distribution $Pr_\theta(y)$ and a sample $y_1, \ldots, y_N$, the log-likelihood is:

$$L(\theta) = \sum_{i=1}^{N} \log Pr_\theta(y_i)$$

The MLE finds $\hat{\theta} = \arg\max_\theta L(\theta)$.

> [!IMPORTANT]
> We typically assume a distribution family (e.g., normal), since the true distribution is unknown. The normal distribution is often a good assumption.

## MLE Under Normal Distribution

Assuming $Pr(Y | X, \theta) = \mathcal{N}(f_\theta(X), \sigma^2)$, the log-likelihood becomes:

$$L(\theta) = -N \cdot \log(\sigma) - \frac{N}{2} \log(2\pi) - \frac{1}{2\sigma^2} \sum_{i=1}^{N} (y_i - f_\theta(\vec{x}_i))^2$$

The first two terms are constants ($C_2$ and part of $C_1$). Therefore:

$$L(\theta) = RSS(\theta) \cdot C_1 + C_2$$

> [!IMPORTANT]
> For linear models with normally distributed errors, maximizing the likelihood is equivalent to minimizing [[Loss Functions in Machine Learning|RSS]]. This provides a probabilistic justification for least squares regression.

## Cross-Entropy Loss

For classification with $K$ classes where $Pr(Y = y_k | X = \vec{x}) = p_{k,\theta}(\vec{x})$:

$$L(\theta) = \sum_{i=1}^{N} \log(p_{y_i, \theta}(\vec{x}_i))$$

The negative log-likelihood $-L(\theta)$ is the **cross-entropy loss**, commonly used as the loss function for classification models like [[Logistic Regression]].

## Role in Model Selection

MLE finds the best parameters within a model, but comparing models of different complexity requires additional criteria. Pure likelihood always favors more complex models, leading to [[Overfitting]]. This motivates penalized approaches like:
- [[Bayesian Information Criterion]]: penalizes model complexity
- [[Minimum Description Length]]: selects the model with the shortest encoding

## Related Concepts

- [[Loss Functions in Machine Learning]]: MLE with normal assumption recovers RSS minimization
- [[Linear Regression]]: MLE provides a probabilistic interpretation of least squares
- [[Logistic Regression]]: uses MLE with cross-entropy loss for classification
- [[Bayesian Information Criterion]]: uses MLE as a building block for model selection
- [[Overfitting]]: pure MLE without regularization overfits complex models
