---
title: 3D Data Acquisition
aliases:
  - Gewinnung von 3D-Daten
  - 3D Scanning
tags:
  - visual-computing
  - 3d-visualization
description: "Methods for capturing real-world 3D geometry including laser scanning, satellite imagery, and medical imaging"
draft: false
---

> [!NOTE] Definition
> 3D data acquisition captures real-world geometry using various sensing technologies, each suited to different scales and applications.

## Methods

| Method | Description |
|--------|-------------|
| **Height measurement / Satellite imagery** | Large-scale terrain data from aerial or space sensors |
| **Laser scanning** | Projects laser beams onto surfaces; does not require physical contact |
| **MRI / CT** | Medical imaging producing comprehensive 3D volumetric data; may require indirect contact depending on the device |

## Triangulation Requirements

Preferred properties for the resulting triangle meshes:
- **Equilateral triangles** (all angles 60 degrees)
- **Node degree 6** (each vertex connected to 6 edges)

## Related Concepts

- [[Voronoi Diagram]]: partitioning acquired point clouds
- [[Delaunay Triangulation]]: triangulating acquired point sets
- [[Volume Rendering]]: visualizing acquired volumetric data (MRI/CT)
