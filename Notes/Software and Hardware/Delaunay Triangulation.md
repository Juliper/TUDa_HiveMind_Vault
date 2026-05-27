---
title: Delaunay Triangulation
aliases:
  - Delaunay-Triangulation
tags:
  - visual-computing
  - 3d-visualization
description: "Triangulation of a point set where no point lies inside the circumcircle of any triangle"
draft: false
---

> [!NOTE] Definition
> Delaunay triangulation connects a set of points into triangles such that no point lies inside the circumcircle of any triangle. It is the dual of the [[Voronoi Diagram]].

## Construction from Voronoi Diagram

1. Start with the Voronoi diagram of the point set
2. Connect points from adjacent Voronoi cells with edges
3. These edges form the Delaunay triangles

## Preferred Properties

- **Equilateral triangles** (all angles close to 60 degrees) are preferred
- **Node degree 6** is the ideal connectivity

## Edge Flipping

If a point (other than the triangle's own vertices) lies inside the circumcircle of a triangle, the shared edge must be flipped to restore the Delaunay property.

> [!IMPORTANT]
> To perform Delaunay triangulation on a 3D point cloud, the points must first be projected onto a 2D plane.

## Related Concepts

- [[Voronoi Diagram]]: the dual spatial partition
- [[Mesh Processing]]: further operations on the resulting triangle mesh
- [[Volume Rendering]]: triangulated surfaces for indirect visualization
