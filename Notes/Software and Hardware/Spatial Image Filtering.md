---
title: Spatial Image Filtering
aliases:
  - Bildfilterung
  - Image Filtering
  - Filtermasken
tags:
  - visual-computing
  - image-processing
description: "Neighborhood-based image operations using filter kernels in spatial and frequency domains"
draft: false
---

> [!NOTE] Definition
> Image filtering modifies pixel values based on their neighborhood using filter kernels (masks). Filters can operate in the spatial domain (convolution) or frequency domain (multiplication).

## Spatial Domain (Convolution)

### Low-Pass Filters (Tiefpass)

Smooth the image by emphasizing low-frequency components:

- **Mean filter**: averages values in a sliding window to reduce noise
- **Gaussian filter**: weighted averaging considering spatial distribution, preserves image quality better
- **Median filter**: replaces each pixel with the median of its neighbors

| Property | Value |
|----------|-------|
| Coefficients | All positive, sum = 1 |
| Output | Only positive values |
| Effect | Removes noise, blurs edges |

> [!WARNING]
> The median filter is **non-linear** (requires sorting) and therefore **cannot** be expressed as a convolution.

### High-Pass Filters (Hochpass)

Emphasize edges and rapid intensity changes:

- **Difference filter**: computes first derivative (partial gradients)
- **Laplacian filter**: computes second derivative, emphasizes edges, contours, and structures

| Property | Value |
|----------|-------|
| Coefficients | Positive and negative, sum = 0 |
| Output | Positive and negative values |
| Effect | Enhances edges, amplifies noise |

## Frequency Domain

Filtering via [[Fourier Transform]] and the [[Convolution Theorem]]:

| Filter Type | Action | Effect |
|-------------|--------|--------|
| Low-pass | Cut high frequencies | Less noise, more blur |
| High-pass | Cut low frequencies | Sharp transitions emphasized |
| Band-pass | Keep frequencies within a range | Selective frequency isolation |

> [!IMPORTANT]
> Frequency domain filtering offers fast computation and simple handling, but spatial domain filters are only approximations of ideal frequency-domain filters.

## Related Concepts

- [[Convolution Theorem]]: mathematical basis for spatial filtering
- [[Pixel Operations]]: point-wise operations (no neighborhood)
- [[Image Deblurring]]: using filters to reverse blur
- [[Wiener Filter]]: an optimal deblurring filter
