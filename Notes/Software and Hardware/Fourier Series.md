---
title: Fourier Series
aliases:
  - Fourier-Reihe
tags:
  - visual-computing
  - signal-processing
description: "Representation of periodic functions as sums of sine and cosine terms"
draft: false
---

> [!NOTE] Definition
> A Fourier series represents a periodic function as an infinite sum of sine and cosine functions with different frequencies and amplitudes.

## Dirichlet Conditions

A function can be represented as a Fourier series if:
1. The number of discontinuities within one period is finite
2. The number of extrema within one period is finite
3. The function is integrable over each period (finite area)

## Definition

For a function with period $2\pi$:

$$f(x) = a_0 + \sum_{n=1}^{\infty} (a_n \cos(nx) + b_n \sin(nx))$$

### Coefficients

$$a_n = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x) \cos(nx) \, \mathrm{d}x$$

$$b_n = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x) \sin(nx) \, \mathrm{d}x$$

## Symmetry Properties

| Function Type | Condition | Result |
|--------------|-----------|--------|
| Even | $f(x) = f(-x)$ | All $b_n = 0$ (only cosine terms) |
| Odd | $f(-x) = -f(x)$ | All $a_n = 0$ (only sine terms) |

## Complex Fourier Series

$$f(x) = a_0 + \sum_{n=1}^{\infty} (a_n \cos(nx) + b_n \sin(nx)) = \sum_{n=-\infty}^{\infty} c_n e^{inx}$$

## Related Concepts

- [[Fourier Transform]]: extension to non-periodic functions
- [[Convolution Theorem]]: connecting spatial and frequency domains
