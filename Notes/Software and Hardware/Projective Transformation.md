---
title: Projective Transformation
aliases:
  - Projektion
  - Projektive Abbildung
  - Projection
tags:
  - visual-computing
  - computer-graphics
description: "Non-affine transformations that project 3D scenes onto 2D, including perspective and parallel projection"
draft: false
---

> [!NOTE] Definition
> Projective transformations map 3D scenes onto 2D surfaces. Unlike [[Affine Transformation]]s, they do not preserve parallelism (in the perspective case).

## Properties of Projective Mappings

1. Lines map to lines
2. Intersections of lines are preserved
3. Surfaces map to surfaces
4. Order of points on projective lines is preserved

## Perspective Projection

Projects toward a single vanishing point (Center of Projection - COP):

| Property | Preserved? |
|----------|-----------|
| Lines to lines | Yes |
| Bounded objects stay bounded | Yes |
| Length ratios | **No** - they change |
| Angles | **No** - they change |
| Parallelism | **No** - parallels converge |

Produces "natural" depth perception. Used in games, film, and most 3D applications.

## Parallel Projection

Projects along a Direction of Projection (DOP) with parallel rays:

| Property | Preserved? |
|----------|-----------|
| Parallelism | Yes |
| Angles | **No** |

Used in medical imaging where depth distortion is undesirable.

### Classical Projection Types

- Front view (Frontansicht)
- Cabinet projection (Kabinettperspektive)
- General parallel projection
- Isometric perspective
- Central perspective (Zentralperspektive)
- Bird's eye view (Vogelperspektive)

## Canonical View Volume

$$\text{Perspective Projection} = \text{Parallel Projection} \cdot \text{Perspective Transformation}$$

## 3D Interaction with 2D Input

**Problem**: mapping a 2D input device to 3D operations creates ambiguity (infinitely many 3D positions map to the same 2D cursor position).
**Solution**: use manipulators (handles, gizmos) to constrain interaction axes.

## Related Concepts

- [[Affine Transformation]]: the subset of transformations that preserve parallelism
- [[Graphics Pipeline]]: projection occurs in the geometry processing stage
- [[Depth Cue Theory]]: perspective projection provides depth cues
