---
title: Image Histogram
aliases:
  - Histogramm
  - Brightness Histogram
tags:
  - visual-computing
  - image-processing
description: "Diagram showing the distribution of brightness values in an image"
draft: false
---

> [!NOTE] Definition
> An image histogram displays the frequency distribution of brightness values. The x-axis represents brightness (typically 0-255), the y-axis represents the number of pixels at each value.

## What It Reveals

- Contrast, brightness, over- and underexposure
- Overall tonal distribution of the image

## Image Properties from Histogram

| Property | Definition |
|----------|-----------|
| **Image dynamics** (Bilddynamik) | Range of real light intensities mapped to the grayscale |
| **Image contrast** (Bildkontrast) | Range of the grayscale used to represent image information |
| **Image brightness** (Bildhelligkeit) | Illumination intensity (grayscale value) |

### Derived Measures

- Image brightness = **mean** of all grayscale values
- Image contrast = **variance** of all grayscale values

## Related Concepts

- [[Pixel Operations]]: histogram equalization and other transformations
- [[Digital Image Pipeline]]: histograms are used to evaluate captured images
