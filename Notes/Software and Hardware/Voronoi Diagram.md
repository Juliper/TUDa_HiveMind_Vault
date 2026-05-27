---
title: Voronoi Diagram
aliases:
  - Voronoi-Diagramm
tags:
  - visual-computing
  - 3d-visualization
description: "Spatial partitioning where each region contains all points closest to a given seed point"
draft: false
---

> [!NOTE] Definition
> A Voronoi diagram partitions space into regions (cells) such that each cell contains all points closest to its associated seed point. Cells are separated by lines equidistant from neighboring seed points.

## Construction

For a set of projected points:
1. For each point, determine all locations that are closer to it than to any other point
2. These locations form the Voronoi cell for that point
3. Cell boundaries are the perpendicular bisectors between neighboring points

## Relationship to Delaunay Triangulation

Voronoi diagrams and [[Delaunay Triangulation]]s are **dual** to each other:

- **Voronoi $\rightarrow$ Delaunay**: connect the centers of neighboring Voronoi cells with lines; these centers become the triangle vertices
- **Delaunay $\rightarrow$ Voronoi**: the circumcenters of the triangles become Voronoi vertices; the perpendicular bisectors of triangle edges form cell boundaries

## Related Concepts

- [[Delaunay Triangulation]]: the dual triangulation
- [[Volume Rendering]]: Voronoi diagrams help structure volumetric data
