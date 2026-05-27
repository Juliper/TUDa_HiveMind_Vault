---
title: X3DOM
aliases:
  - X3D
  - Extensible 3D
tags:
  - visual-computing
  - computer-graphics
  - web
description: "Declarative markup language for rendering 3D scenes in HTML using scene graphs"
draft: false
---

> [!NOTE] Definition
> X3DOM (Extensible 3D Document Object Model) is a declarative markup language for representing 3D scenes in web browsers, based on XML syntax.

## Motivation

- Many applications need 3D in the browser (reconstruction, modeling, etc.)
- Challenges: efficiency with large datasets, portability across devices
- Goal: simple integration and interaction with 3D graphics in HTML

## The HTML Problem

[[Scene Graph]]s are DAGs (nodes can have multiple parents), but HTML's DOM is a **tree** structure (each element has exactly one parent).

**Solution**: the **DEF/USE mechanism**
- Define a node once with `DEF = X`
- Reuse it anywhere with `USE = X`

## Scene Graph in X3DOM

Properties of the X3DOM scene graph:
- Directed and acyclic
- Single root
- Not a tree (nodes can have multiple parents via DEF/USE)
- Uses XML syntax

## Related Concepts

- [[Scene Graph]]: the underlying data structure
- [[Graphics Pipeline]]: the rendering pipeline X3DOM feeds into
