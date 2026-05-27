---
title: Signal Sampling and Aliasing
aliases:
  - Abtastung
  - Aliasing
  - Nyquist Theorem
  - Whittaker-Shannon Theorem
tags:
  - visual-computing
  - signal-processing
description: "Discretization of continuous signals and the aliasing artifacts that occur when sampling rate is too low"
draft: false
---

> [!NOTE] Definition
> Sampling is the discretization of a continuous function using a comb function. Aliasing occurs when the sampling rate is insufficient to capture the signal's frequency content.

## Discrete Sampling

$$\hat{f}(x) = f(x) \cdot \sum_{n=-\infty}^{\infty} \delta(x - n \cdot \delta x)$$

## Nyquist-Shannon Theorem

> [!IMPORTANT]
> The sampling frequency must be at least **twice** the highest frequency contained in the signal to avoid aliasing. A frequency can be reconstructed without error if the sampling interval $\delta x^{-1}$ is at least double the cutoff frequency.

## Aliasing in Signal Processing

When a signal is sampled at too low a frequency:
- Higher frequencies are incorrectly interpreted as lower frequencies
- The original signal cannot be fully reconstructed
- This leads to distortions in the reconstructed signal

## Aliasing in Computer Graphics

When a screen pixel tries to represent more information than it can display:
- Visible staircase patterns on object edges ("jaggies" / Treppeneffekt)
- **Anti-aliasing** techniques mitigate this by averaging neighboring pixel values to produce smoother transitions

## Related Concepts

- [[Fourier Transform]]: the frequency-domain analysis underlying sampling theory
- [[Digital Image Pipeline]]: where sampling occurs in image acquisition
- [[Spatial Image Filtering]]: filtering to prevent aliasing
