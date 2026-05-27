---
title: Image Deblurring
aliases:
  - Scharfen
  - Deblurring
  - Image Sharpening
tags:
  - visual-computing
  - image-processing
description: "Techniques for reversing blur in images, including inverse filtering and regularization approaches"
draft: false
---

> [!NOTE] Definition
> Image deblurring (sharpening) attempts to reverse the blur operation to recover the original sharp image. It is fundamentally an ill-posed problem.

## Basic Approach - Inverse Filter

Given a blurred image $G = A \cdot F$ where $A$ is the blur filter and $F$ is the original:

$$F = G \cdot A^{-1}$$

### Problem 1: Numerical Precision

Values cannot always be stored with infinite precision. The inverse filter amplifies noise in the imaginary part. Solution: use the complex conjugate matrix $A^*$:

$$F = A^{-1} \cdot G = \frac{A^*}{A^* A} \cdot G = \frac{A^*}{|A|^2} \cdot G$$

### Problem 2: Noise Amplification

Every image contains noise. The inverse filter not only fails to remove noise but amplifies small deviations into large artifacts. Solution: use regularized filters like the [[Wiener Filter]].

## Hadamard Well-Posedness

A mathematical problem is well-posed if:
1. **Existence**: a solution exists
2. **Uniqueness**: the solution is unique
3. **Stability**: small changes in input cause only small changes in output

> [!IMPORTANT]
> Blurring is a well-posed problem. Deblurring is **ill-posed** - small input changes can cause drastic output changes. This is why regularization is essential.

## Scale-Space Sharpening

Subtracting the Laplace operator:

$$L_{\text{sharp}} = L_0 - t(L_{xx} + L_{yy}) = L_0 - t\delta L$$

Higher-order terms can be added for refinement, but too many additional terms can degrade results.

## Related Concepts

- [[Wiener Filter]]: single-step regularized deblurring
- [[Perona-Malik Diffusion]]: multi-step edge-preserving deblurring
- [[Total Variation Denoising]]: optimization-based approach with distance penalty
- [[Spatial Image Filtering]]: general filtering framework
