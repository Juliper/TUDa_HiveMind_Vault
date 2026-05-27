---
title: Fourier Transform
aliases:
  - Fourier-Transformation
  - FT
tags:
  - visual-computing
  - signal-processing
description: "Decomposes a function into its frequency components by transforming from spatial to frequency domain"
draft: false
---

> [!NOTE] Definition
> The Fourier Transform decomposes a function (signal) into its constituent frequency components, mapping from the spatial/time domain to the frequency domain.

## Forward Transform

$$F(u) = \int_{-\infty}^{\infty} f(t) e^{-2\pi i u x} \, \mathrm{d}x$$

## Inverse Transform

$$f(x) = \int_{-\infty}^{\infty} F(u) e^{+2\pi i u x} \, \mathrm{d}u$$

## Key Properties

- Decomposes any signal into a sum of sinusoidal components
- Reversible - the original function can be perfectly reconstructed
- Fundamental tool for analyzing frequency content of images and signals

## Complex Numbers (Prerequisites)

$$z = a + ib = r \cdot e^{i\varphi} = r \cdot (\cos(\varphi) + i\sin(\varphi))$$

$$\varphi = \arctan\left(\frac{b}{a}\right), \quad r = |z|, \quad i := \sqrt{-1}$$

## Related Concepts

- [[Fourier Series]]: the periodic function version
- [[Convolution Theorem]]: convolution in spatial domain equals multiplication in frequency domain
- [[Signal Sampling and Aliasing]]: discretizing continuous signals
- [[Spatial Image Filtering]]: applying filters in frequency domain
