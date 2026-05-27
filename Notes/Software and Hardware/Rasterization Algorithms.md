---
title: Rasterization Algorithms
aliases:
  - Rasterisierung
  - Rasterization
tags:
  - visual-computing
  - computer-graphics
description: "Algorithms for converting geometric primitives into pixel representations - Bresenham, Scanline, and Z-Buffer"
draft: false
---

> [!NOTE] Definition
> Rasterization converts continuous geometric primitives (lines, polygons) into discrete pixel representations on screen.

## Bresenham's Line Algorithm

Draws lines on a pixel grid by computing the $x$ and $y$ difference between start and end positions, then advancing along the fast direction ($x$) and conditionally stepping in the slow direction ($y$).

Number of pixels drawn: $\max(|x_1 - x_0|, |y_1 - y_0|) + 1$

## Scanline Algorithm

Fills polygons by scanning horizontal lines from top to bottom:
1. Process each horizontal scanline
2. Determine where the scanline intersects polygon edges
3. Fill pixels between intersection pairs

## Z-Buffer Algorithm

Handles visibility (occlusion) at the pixel level:
- Maintains a depth buffer storing the closest $z$-value for each pixel
- For each polygon fragment, compare its $z$-value to the buffer
- Only draw if the fragment is closer than what's already stored

| Property | Detail |
|----------|--------|
| Handles any object type | Yes |
| Independent of depth complexity | Yes |
| Supports incremental scene updates | Yes |
| Hardware implementation | Easy |
| Transparency support | No |
| Precision | Limited by buffer depth |

## Painter's Algorithm

Alternative to z-buffer: sort all primitives by $z$-value (back-to-front) and draw in that order. Later draws overwrite earlier ones.

> [!WARNING]
> The Painter's Algorithm fails with overlapping polygons that form cycles and cannot handle transparency correctly.

## Related Concepts

- [[Graphics Pipeline]]: rasterization is the third pipeline stage
- [[Spatial Data Structures in Computer Graphics]]: culling before rasterization
- [[Shading Models]]: computing colors for rasterized pixels
