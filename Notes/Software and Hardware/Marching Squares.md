---
title: Marching Squares
aliases:
  - Marching-Squares
tags:
  - visual-computing
  - 3d-visualization
description: "Algorithm for extracting contour lines from 2D scalar fields by classifying grid cell corners"
draft: false
---

> [!NOTE] Definition
> Marching Squares extracts contour lines from a 2D scalar field by classifying the corners of each grid cell as inside or outside a threshold, then connecting boundary crossings.

## How It Works

1. For each grid square, classify each corner as "white" (above threshold) or "black" (below threshold)
2. Based on the corner classification pattern, determine where the contour crosses the cell edges
3. Connect the crossings to form contour segments

> [!WARNING]
> The algorithm is **not always unambiguous** - when diagonally opposite corners have the same classification, there are two valid ways to connect the contour segments (saddle point ambiguity).

## Related Concepts

- [[Mesh Processing]]: further refinement of extracted contours
- [[Volume Rendering]]: Marching Squares is the 2D analog of Marching Cubes used in volumetric data
