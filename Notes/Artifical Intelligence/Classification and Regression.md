---
title: Classification and Regression
aliases:
  - Klassifikation und Regression
  - Supervised Learning Tasks
tags:
  - machine-learning
  - supervised-learning
description: "The two fundamental supervised learning tasks - predicting discrete labels (classification) or continuous values (regression)"
draft: false
---

> [!NOTE] Definition
> In supervised learning, each observation $\vec{x}$ has an associated label $y$, forming pairs $(\vec{x}, y) \in X \times Y$. The task is to learn a function $\hat{f}$ that approximates the true function $f: X \to Y$ from a finite set of training examples.

## The Two Tasks

| | Classification | Regression |
|---|---|---|
| **Output space** $Y$ | Discrete (finite set of classes) | Continuous ($Y = \mathbb{R}$) |
| **Goal** | Predict a category/label | Predict a numerical value |
| **Example** | Is this email spam or not? | What is the house price? |
| **From regression model** | Apply threshold: $\hat{y} = +1$ if $\hat{f}(\vec{x}) \geq \theta$, else $-1$ | Direct output $\hat{y} = \hat{f}(\vec{x})$ |

## Formal Setup

Given a set of $N$ examples $\mathbf{X} = \{\vec{x}_1, \ldots, \vec{x}_N\}$ where each $\vec{x}_i$ is a $p$-dimensional vector, represented as an $(N \times p)$-matrix:

$$\mathbf{X} = \begin{pmatrix} x_{1,1} & x_{1,2} & \cdots & x_{1,p} \\ x_{2,1} & \ddots & & \vdots \\ \vdots & & & \vdots \\ x_{N,1} & x_{N,2} & \cdots & x_{N,p} \end{pmatrix}$$

We seek a function $\hat{f}$ (the learned **model**) that for new data $\vec{x} \in X$ produces a prediction $\hat{y} = \hat{f}(\vec{x}) \in Y$.

> [!IMPORTANT]
> We only have a finite subset of observations (training data) from the true function $f$. The challenge is to learn $\hat{f}$ that generalizes beyond the training set - this is what separates learning from memorization.

## Related Concepts

- [[Linear Regression]]: a fundamental regression model
- [[K-Nearest Neighbors]]: can be used for both classification and regression
- [[Loss Functions in Machine Learning]]: different loss functions are used for classification vs regression
- [[Overfitting]]: the central challenge in supervised learning
