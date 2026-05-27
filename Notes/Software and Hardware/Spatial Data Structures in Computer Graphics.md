---
title: Spatial Data Structures in Computer Graphics
aliases:
  - Raumliche Datenstrukturen
  - Culling Techniques
tags:
  - visual-computing
  - computer-graphics
description: "Data structures and techniques for efficiently determining visibility and occlusion in 3D scenes"
draft: false
---

> [!NOTE] Definition
> Spatial data structures organize 3D scene data to efficiently determine which objects are visible, enabling culling of invisible geometry to improve rendering performance.

## Culling Techniques

Removing invisible geometry from the rendering pipeline:

| Technique | Description |
|-----------|-------------|
| **Backface Culling** | Don't render the back side of objects (self-occluded) |
| **View Frustum Culling** | Don't render objects outside the camera's view cone |
| **Occlusion Culling** | Don't render objects hidden behind other objects |
| **Clipping** | Cut away parts of objects outside the view boundary |

## Spatial Subdivision Trees

| Structure | Method |
|-----------|--------|
| **k-d Tree** | Splits space into two regions via vertical or horizontal lines |
| **Quadtree** | Splits space into four equal regions |
| **BSP Tree** | Binary Space Partitioning - arbitrary split into two regions |

## Bounding Volumes

Simplified enclosing shapes for fast intersection tests:

- **Sphere**: simplest, but loose fit
- **Bounding Box** (AABB): axis-aligned box
- **Oriented Bounding Box** (OBB): rotated to fit the object more tightly

> [!IMPORTANT]
> View Frustum Culling can use k-d Trees for efficient spatial queries.

## Related Concepts

- [[Graphics Pipeline]]: culling happens in the geometry processing stage
- [[Rasterization Algorithms]]: the z-buffer handles per-pixel visibility after culling
- [[3D Data Representation]]: the primitives being organized by these structures
