---
title: Total Variation Denoising
aliases:
  - Totale Variation
  - TV Denoising
tags:
  - visual-computing
  - image-processing
description: "Optimization-based denoising that penalizes deviation from the original image, solving the stopping problem of Perona-Malik"
draft: false
---

> [!NOTE] Definition
> Total Variation denoising solves the stopping problem of [[Perona-Malik Diffusion]] by adding a distance penalty that penalizes deviation from the original image. The algorithm naturally terminates at the optimal solution.

## How It Works

- Minimizes total variation (smoothness) of the image
- Adds a **distance penalty** term measuring deviation from the original image
- The penalty prevents over-smoothing by keeping the result close to the input

> [!IMPORTANT]
> Unlike Perona-Malik, no explicit stopping time is needed - the algorithm terminates at the optimal solution automatically.

## Comparison with Other Methods

| Method | Stopping | Adaptivity |
|--------|----------|------------|
| [[Wiener Filter]] | Single step | Global R parameter |
| [[Perona-Malik Diffusion]] | Manual stopping time | Local via gradient |
| **Total Variation** | Automatic (optimal) | Distance penalty |

## Related Concepts

- [[Perona-Malik Diffusion]]: the multi-step method whose stopping problem TV solves
- [[Image Deblurring]]: the general deblurring and denoising framework
