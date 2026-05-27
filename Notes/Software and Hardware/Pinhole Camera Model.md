---
title: Pinhole Camera Model
aliases:
  - Lochkamera-Modell
tags:
  - visual-computing
  - computer-vision
description: "Simplest camera model projecting 3D scenes onto a 2D image plane through a single point"
draft: false
---

> [!NOTE] Definition
> The pinhole camera model describes image formation by projecting light rays from a 3D scene through a single point (the pinhole) onto an image plane, producing an inverted image.

## How It Works

```mermaid
flowchart LR
    A[3D Scene] -->|Light rays| B[Pinhole] -->|Inverted projection| C[Image Plane]
```

- Light from the scene passes through a tiny aperture
- Each point in the scene maps to exactly one point on the image plane
- The resulting image is **inverted** (flipped vertically and horizontally)
- A virtual image forms on the opposite side of the pinhole

## Challenges in Recognition

- How do we recognize shapes, depth, and objects from a 2D projection?
- The level of detail in an image can fundamentally change its interpretation

## Related Concepts

- [[Bayes Decision Theory in Computer Vision]]: classifying objects in projected images
- [[Projective Transformation]]: the mathematical framework for projection
- [[Digital Image Pipeline]]: how modern cameras digitize the projected image
