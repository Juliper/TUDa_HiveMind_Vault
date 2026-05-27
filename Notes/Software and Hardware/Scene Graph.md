---
title: Scene Graph
aliases:
  - Szenengraph
  - Szenengraphen
tags:
  - visual-computing
  - computer-graphics
description: "Directed acyclic graph structuring 3D scene data including geometry, transformations, materials, and lights"
draft: false
---

> [!NOTE] Definition
> A scene graph is a directed acyclic graph (DAG) that structures 3D scene data hierarchically, organizing geometry, transformations, materials, camera positions, lights, and special effects.

## Structure

**Root to leaves**: Grouping $\rightarrow$ Transformation $\rightarrow$ Object

The graph is traversed node by node, with operations depending on node type:

| Node Type | Operation |
|-----------|-----------|
| **Grouping** | Traverse child nodes if the group is active |
| **Transformation** | Apply transformation matrix $M$ to the Current Transformation Matrix (CTM) |
| **Object** | Draw the object using the current CTM |

## Properties

- Directed and acyclic
- Single root node
- **Not a tree** - nodes can have multiple parents (enables reuse)

## Advantages

- **Reusability** of object data
- **Semantic grouping** of related objects
- **Transformation hierarchy** enables transforming entire groups at once

## Related Concepts

- [[X3DOM]]: scene graphs in HTML using X3D
- [[Affine Transformation]]: transformations stored in scene graph nodes
- [[Graphics Pipeline]]: the scene graph feeds into the rendering pipeline
