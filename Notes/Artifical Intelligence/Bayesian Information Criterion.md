---
title: Bayesian Information Criterion
aliases:
  - BIC
  - Bayes Informationskriterium
  - Bayesian Model Selection
tags:
  - machine-learning
  - model-selection
  - statistics
description: "A model selection criterion that balances likelihood fit against model complexity using a logarithmic penalty"
draft: false
---

> [!NOTE] Definition
> The Bayesian Information Criterion (BIC) is a model selection criterion derived from approximating the posterior probability of a model. It penalizes model complexity to prevent [[Overfitting]], favoring simpler models that explain the data well.

## Bayesian Model Selection

Given models $\mathcal{M}_1, \ldots, \mathcal{M}_M$ with parameters $\theta_m$ and training data $\mathcal{T}$, the posterior probability of a model is:

$$Pr(\mathcal{M}_m | \mathcal{T}) \sim Pr(\mathcal{M}_m) \cdot Pr(\mathcal{T} | \mathcal{M}_m)$$

To compare two models, we compute the ratio:

$$\frac{Pr(\mathcal{M}_m | \mathcal{T})}{Pr(\mathcal{M}_l | \mathcal{T})} = \frac{Pr(\mathcal{M}_m)}{Pr(\mathcal{M}_l)} \cdot \frac{Pr(\mathcal{T} | \mathcal{M}_m)}{Pr(\mathcal{T} | \mathcal{M}_l)}$$

If the ratio is greater than 1, we prefer $\mathcal{M}_m$.

### Approximating the Evidence

Assuming equal priors and using [[Maximum Likelihood Estimation|MLE]] to estimate parameters:

$$\log Pr(\mathcal{T} | \mathcal{M}_i) \approx \log Pr(\mathcal{T} | \hat{\theta}_i, \mathcal{M}_i) - \frac{d_i}{2} \cdot \log N + O(1)$$

where $d_i$ is the number of free parameters and $N$ is the number of data points.

## BIC Formula

$$BIC = -2 \cdot loglik + (\log N) \cdot d$$

where $loglik = \sum_{i=1}^{N} \log Pr_{\hat{\theta}}(y_i)$ is the maximized log-likelihood.

| Component | Meaning |
|---|---|
| $-2 \cdot loglik$ | Measures how well the model fits the data (lower = better fit) |
| $(\log N) \cdot d$ | Penalty for model complexity (increases with more parameters) |

> [!IMPORTANT]
> Select the model with the **smallest BIC**. This corresponds to the model with the greatest approximate posterior probability.

## Relative Model Quality

Given $M$ models, the relative probability of model $m$ is:

$$\frac{e^{-\frac{1}{2} \cdot BIC_m}}{\sum_{l=1}^{M} e^{-\frac{1}{2} \cdot BIC_l}}$$

This allows ranking all candidate models, not just pairwise comparison.

## Connection to MDL

BIC is closely related to the [[Minimum Description Length]] principle: the model with the smallest BIC also has the shortest code length under MDL. Minimizing BIC is equivalent to minimizing the description length of the data.

## Related Concepts

- [[Maximum Likelihood Estimation]]: BIC builds on the maximized log-likelihood
- [[Minimum Description Length]]: equivalent model selection perspective from information theory
- [[Cross-Validation]]: alternative model selection approach based on error minimization
- [[Overfitting]]: BIC's complexity penalty prevents overfitting
