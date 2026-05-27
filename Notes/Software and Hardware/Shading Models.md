---
title: Shading Models
aliases:
  - Beleuchtungsmodelle
  - Shading
tags:
  - visual-computing
  - computer-graphics
description: "Methods for computing surface brightness in 3D rendering - Flat, Gouraud, and Phong shading"
draft: false
---

> [!NOTE] Definition
> Shading models determine how the brightness of a 3D surface is calculated based on its orientation relative to light sources. The three classic models trade quality for computational cost.

## Comparison

| Model | Normal Computation | Interpolation | Quality |
|-------|-------------------|---------------|---------|
| **Flat** | One normal per primitive | None | Faceted appearance |
| **Gouraud** | Normals at vertices | Brightness values interpolated linearly | Smooth but misses specular highlights |
| **Phong** | Normals at vertices | Normal vectors interpolated and normalized per pixel | Smooth with accurate specular highlights |

## Phong Illumination Model

The total light intensity at a point is the sum of three components:

$$I_{\text{total}} = \text{Ambient} + \text{Diffuse} + \text{Specular}$$

- **Ambient**: constant background illumination
- **Diffuse**: light scattered equally in all directions (depends on angle between surface normal and light direction)
- **Specular**: mirror-like reflection (depends on viewing angle)

## Related Concepts

- [[Graphics Pipeline]]: shading occurs in the geometry/rasterization stages
- [[Rasterization Algorithms]]: pixel-level operations that apply shading values
- [[3D Data Representation]]: the primitives being shaded
