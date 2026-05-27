---
title: Affine Transformation
aliases:
  - Affine Abbildung
  - Affine Transformationen
tags:
  - visual-computing
  - computer-graphics
description: "Linear transformations preserving parallelism and ratios - translation, rotation, scaling, and shearing"
draft: false
---

> [!NOTE] Definition
> Affine transformations are geometric mappings that preserve lines, parallelism, and ratios of distances. They include translation, rotation, scaling, and shearing.

## Properties

1. Lines map to lines
2. Bounded objects remain bounded
3. Ratios of lengths, areas, and volumes are preserved
4. Parallel objects remain parallel

## Types

| Transformation | Matrix Characteristic |
|---------------|----------------------|
| Translation | Identity + translation vector |
| Rotation | Orthogonal matrix |
| Scaling | Diagonal matrix (all off-diagonal elements are zero) |
| Shearing | Triangular matrix |

## Composition

The order of application matters: **composition of affine transformations is not commutative**.

Standard order: Translation $\rightarrow$ Scaling $\rightarrow$ Rotation

### How to Rotate Around an Arbitrary Point

1. Translate the rotation center to the origin
2. Apply rotation
3. Translate back to the rotation center

In matrix form: $M = T \cdot R \cdot T^{-1}$ (applied right-to-left: step 3 $\cdot$ step 2 $\cdot$ step 1)

## Transformation Pipeline in Graphics

1. **Modeling Transformation**: arrange 3D objects in world space
2. **Viewing Transformation**: position the camera
3. **Projection Transformation**: project to 2D (note: this is **not** affine)
4. **Viewport Transformation**: map to screen coordinates

## Related Concepts

- [[Projective Transformation]]: non-affine projection that does not preserve parallelism
- [[Graphics Pipeline]]: where transformations are applied
- [[3D Data Representation]]: the geometric data being transformed
