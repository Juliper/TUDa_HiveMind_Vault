---
title: Digital Image Pipeline
aliases:
  - Digitale Kamera
  - Digital Camera Pipeline
tags:
  - visual-computing
  - image-processing
description: "The process chain from real-world scene capture to digital image representation"
draft: false
---

> [!NOTE] Definition
> The digital image pipeline transforms a real-world scene into a digital image through sequential stages of optical capture, digitization, and raster representation.

## Pipeline Stages

```mermaid
flowchart LR
    A[World<br>Real object] --> B[Camera<br>Optical capture] --> C[Digitizer<br>Raster conversion] --> D[Digital Image<br>Pixel array]
```

1. A real-world object is captured by a camera
2. The digitizer converts the light image into a raster arrangement
3. The resulting raster image is the digital photograph

## Image Enhancement Methods

Enhancement can happen in two domains:
- **Spatial domain**: direct manipulation of pixel values
- **Frequency domain**: manipulation via [[Fourier Transform]]

### Possible Improvements
- Correction of camera non-linearities
- Brightness and contrast adjustment
- Emphasizing or suppressing image regions
- Noise removal (e.g., by averaging over $k$ exposures)

## Related Concepts

- [[Image Histogram]]: analyzing the brightness distribution of captured images
- [[Pixel Operations]]: point-wise transformations on pixel values
- [[Spatial Image Filtering]]: neighborhood-based operations on images
- [[Human Visual System]]: the Bayer pattern mimics retinal receptor distribution
