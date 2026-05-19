---
title: Linear Regression
aliases:
  - Lineare Regression
  - Ordinary Least Squares
  - OLS
tags:
  - machine-learning
  - regression
  - linear-models
description: "A model that predicts a target variable as a linear combination of input features, fitted by minimizing the residual sum of squares"
draft: false
---

> [!NOTE] Definition
> Linear regression models the relationship between a response variable $Y$ and input features $\vec{x}$ as a linear function: $y = f(\vec{x}) = \sum_{i=1}^{p} \beta_i x_i + \beta_0$. It is a **global model** - a single set of parameters describes the entire input space.

## Model Formulation

The linear model in compact notation (absorbing $\beta_0$ into $\vec{\beta}$ by prepending a 1 to each $\vec{x}$):

$$y = f(\vec{x}) = \vec{x}^T \vec{\beta} = \langle \vec{x}, \vec{\beta} \rangle$$

where $(x_1, \ldots, x_p) \mapsto (1, x_1, \ldots, x_p)$ and $\vec{\beta} \in \mathbb{R}^{p+1}$.

The function $f$ is determined by the parameter vector $\vec{\beta}$. Learning the model reduces to finding the optimal $\vec{\beta}$.

## Fitting: Ordinary Least Squares

We minimize the [[Loss Functions in Machine Learning|Residual Sum of Squares (RSS)]]:

$$RSS(\vec{\beta}) = \sum_{i=1}^{N} (y_i - \vec{x}_i^T \vec{\beta})^2 = (\vec{y} - \mathbf{X}\vec{\beta})^T(\vec{y} - \mathbf{X}\vec{\beta})$$

This is a **convex** optimization problem, so any local minimum is the global minimum.

### Closed-Form Solution

Taking the partial derivative and setting it to zero:

$$\frac{\partial RSS(\vec{\beta})}{\partial \vec{\beta}} = \mathbf{X}^T(\mathbf{y} - \mathbf{X}\vec{\beta}) = 0$$

If $\mathbf{X}^T\mathbf{X}$ is **regular** (invertible), the optimal solution is:

$$\hat{\vec{\beta}} = (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{y}$$

> [!WARNING]
> $\mathbf{X}^T\mathbf{X}$ must be invertible (non-singular). This fails when features are linearly dependent or when $p > N$ (more features than samples).

## Bias and Variance in Linear Models

The expected in-sample error for a linear model decomposes as:

$$\frac{1}{N}\sum_{i=1}^{N} Err(x_i) = \sigma^2_\epsilon + \frac{p}{N}\sigma^2_\epsilon + \frac{1}{N}\sum_{i=1}^{N}\left[f(\vec{x}_i) - E\hat{f}(\vec{x}_i)\right]^2$$

- **Noise**: $\sigma^2_\epsilon$ (irreducible)
- **Variance**: $\frac{p}{N}\sigma^2_\epsilon$ - grows with number of features $p$, shrinks with data size $N$
- **Bias**: the last term - non-zero when the true relationship is not linear

> [!IMPORTANT]
> Model complexity of a linear model equals the number of parameters $p$ (or $p+1$ with intercept). The [[Curse of Dimensionality]] manifests as increasing variance with more features.

## Limitations

1. Requires the true relationship to be approximately linear
2. [[Curse of Dimensionality]]: with many features, the variance term dominates
3. Data that is not linearly separable will have irreducible bias
4. Model selection is needed since we may not know which features matter

## Related Concepts

- [[Classification and Regression]]: linear regression is the fundamental regression method
- [[Loss Functions in Machine Learning]]: RSS is the loss function for linear regression
- [[Bias-Variance Tradeoff]]: linear models have a clear bias-variance decomposition
- [[K-Nearest Neighbors]]: a local model alternative to global linear models
