---
title: Convolution Theorem
aliases:
  - Faltungssatz
  - Convolution
  - Faltung
tags:
  - visual-computing
  - signal-processing
description: "States that convolution in spatial domain equals multiplication in frequency domain and vice versa"
draft: false
---

> [!NOTE] Definition
> The Convolution Theorem states that convolution in the spatial domain corresponds to multiplication in the frequency domain, and vice versa.

## Convolution Integral

$$h(t) = \int_{-\infty}^{\infty} f(x) g(t - x) \, \mathrm{d}x =: f(t) \circ g(t)$$

A weighted function $g$ is slid over a weighting function $f$ at speed $t$ to smooth the target function. The result $h$ describes the area of overlap between the two functions.

## The Theorem

For two functions $f$ and $g$ with Fourier transforms $F$, $G$, and $H$:

$$H(\xi) = F(\xi) \cdot G(\xi)$$

> [!IMPORTANT]
> - Convolution in spatial domain = multiplication in frequency domain
> - Multiplication in spatial domain = convolution in frequency domain
>
> This is why filtering in the frequency domain (simple multiplication) can be faster than convolution in the spatial domain.

## Related Concepts

- [[Fourier Transform]]: the transform connecting the two domains
- [[Spatial Image Filtering]]: practical application of convolution for image filtering
- [[Wiener Filter]]: a filter designed in frequency domain using this principle
