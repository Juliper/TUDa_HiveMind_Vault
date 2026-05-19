---
title: Loss Functions in Machine Learning
aliases:
  - Error Functions
  - Fehlerfunktionen
  - Residual Sum of Squares
  - RSS
tags:
  - machine-learning
  - optimization
description: "Functions that measure the discrepancy between predicted and true values, used to train and evaluate models"
draft: false
---

> [!NOTE] Definition
> A loss function $L(y, \hat{y})$ quantifies the error between the true value $y$ and the model's prediction $\hat{y}$. The goal of learning is to find model parameters that minimize the expected loss.

## Common Loss Functions

For a learned model $\hat{f}$:

| Loss Function | Formula | Use Case |
|---------------|---------|----------|
| **Absolute error** | $\sum_{i=1}^{N} \|y_i - \hat{y}_i\|$ | Robust to outliers |
| **Squared error (RSS)** | $\sum_{i=1}^{N} (y_i - \hat{y}_i)^2$ | [[Linear Regression]], smooth optimization |
| **0/1 loss** | $\sum_{i=1}^{N} \delta_i$, where $\delta_i = 1$ if $y \neq \hat{y}$, else 0 | [[Classification and Regression|Classification]] |

## Residual Sum of Squares (RSS)

The most common loss for regression, used by [[Linear Regression]]:

$$RSS(\vec{\beta}) = \sum_{i=1}^{N} (y_i - \vec{x}_i^T \vec{\beta})^2 = (\vec{y} - \mathbf{X}\vec{\beta})^T(\vec{y} - \mathbf{X}\vec{\beta})$$

RSS is preferred because:
- It is **differentiable** everywhere (unlike absolute error)
- It defines a **convex** optimization problem
- It has a **closed-form** solution via the normal equation

## Expected Prediction Error (EPE)

Rather than just minimizing the training error, we want to minimize the **expected** error over all possible training sets $\mathcal{T}$:

$$EPE(\hat{f}) = E\left[(Y - \hat{f}(X))^2\right]$$

The optimal solution minimizing EPE is the **regression function**:

$$\hat{f}(x) = E[Y | X = x]$$

> [!IMPORTANT]
> Minimizing training loss alone leads to [[Overfitting]]. The true goal is minimizing the expected prediction error, which decomposes into noise + [[Bias-Variance Tradeoff|bias + variance]].

## Training Error vs. Generalization Error

The training error (in-sample) measures fit on known data. The generalization error (out-of-sample) measures performance on unseen data. [[Cross-Validation]] bridges this gap by estimating generalization error from available data.

## Related Concepts

- [[Linear Regression]]: uses RSS as its loss function
- [[Bias-Variance Tradeoff]]: EPE decomposes into noise, bias, and variance
- [[Overfitting]]: occurs when training loss is minimized at the expense of generalization
- [[Cross-Validation]]: estimates the true generalization error
