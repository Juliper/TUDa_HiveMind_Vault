---
title: Pixel Operations
aliases:
  - Pixeloperationen
  - Point Operations
tags:
  - visual-computing
  - image-processing
description: "Point-wise image transformations that modify individual pixel values independently"
draft: false
---

> [!NOTE] Definition
> Pixel operations transform each pixel value independently, without considering neighboring pixels. They modify the brightness mapping of an image.

## Common Operations

| Operation | Description |
|-----------|-------------|
| **Negation** | Inverts values - black becomes white and vice versa |
| **Binarization** | Values above a threshold become black, all below become white |
| **Windowing** | Only allows grayscale values within a specific brightness range |
| **Contrast stretching** | Maps grayscale values to a new range using a monotonic function, making low-contrast images more visible |
| **Gamma correction** | Non-linear brightness adjustment |
| **Dynamic compression** | Compresses the dynamic range |
| **Histogram equalization** | Redistributes values based on histogram frequency so brightness levels are uniformly distributed |
| **Averaging** | Suppresses uncorrelated noise by averaging over $k$ exposures |

## Related Concepts

- [[Image Histogram]]: the basis for histogram equalization
- [[Spatial Image Filtering]]: neighborhood-based operations (as opposed to point operations)
- [[Digital Image Pipeline]]: pixel operations as part of image enhancement
