---
title: Perona-Malik Diffusion
aliases:
  - Perona Malik
  - Anisotropic Diffusion
tags:
  - visual-computing
  - image-processing
description: "Edge-preserving multi-step denoising method using anisotropic diffusion controlled by gradient strength"
draft: false
---

> [!NOTE] Definition
> Perona-Malik diffusion is a multi-step image processing method that smooths noise while preserving or enhancing edges by making the diffusion rate dependent on the local gradient strength.

## Properties

- Blurs noise
- Preserves or enhances edges
- Uses a smart energy term with a stopping time

## Parameters

### Diffusion Function $c()$

- $c()$ is a function of gradient strength
- Reduces diffusion where edges are present (high gradient)

### Edge Threshold $k$

| $k$ Value | Effect |
|-----------|--------|
| Large $k$ | Only strong edges are preserved |
| Small $k$ | Almost all edges (including noise) are preserved |

## Problems

- The iteration does not stop at the optimal solution automatically
- Signal-to-noise ratio rises and then falls again
- Finding the right stopping point is difficult

**Solution**: A stopping time must be explicitly defined.

## Related Concepts

- [[Total Variation Denoising]]: solves the stopping problem with a distance penalty
- [[Wiener Filter]]: single-step alternative
- [[Image Deblurring]]: the general deblurring framework
