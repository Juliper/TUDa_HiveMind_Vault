---
title: Wiener Filter
aliases:
  - Wiener-Filter
tags:
  - visual-computing
  - image-processing
description: "Optimal single-step deblurring filter using regularization with signal-to-noise ratio parameter R"
draft: false
---

> [!NOTE] Definition
> The Wiener Filter is a single-step deblurring method that regularizes the complex conjugate filter with parameter $R^2$, where $R$ represents the signal-to-noise ratio.

## Behavior by Parameter R

| R Value | Filter Type | Effect |
|---------|-------------|--------|
| Too large | Low-pass | Coarse structures remain, edges blurred, noise removed |
| Too small | High-pass | Coarse structure removed, noise amplified |
| Optimal | Band-pass | Coarse structure preserved, edges enhanced, noise removed |

## Advantages

- Fast computation
- Widely used and well-understood
- Easy to implement

## Disadvantages

- Only one filter for the entire image (no local adaptation)
- No local, region-specific improvements possible
- Only one value of $R$ for the entire image

**Solutions**: local refinements or iterative approaches.

## Related Concepts

- [[Image Deblurring]]: the general deblurring problem
- [[Perona-Malik Diffusion]]: multi-step alternative with edge preservation
- [[Convolution Theorem]]: mathematical basis for frequency-domain filtering
