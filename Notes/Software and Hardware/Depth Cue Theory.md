---
title: Depth Cue Theory
aliases:
  - Depth Cues
  - Tiefenwahrnehmung
tags:
  - visual-computing
  - human-perception
description: "Visual cues the brain uses to perceive depth, distance, and spatial layout"
draft: false
---

> [!NOTE] Definition
> Depth cues are visual signals that the brain uses to estimate the distance, size, and spatial arrangement of objects. They can be combined additively, with different cues carrying different weights.

## Stereoscopy (Binocular Cues)

- **Positive parallax**: convergence lines meet behind the object - object appears farther away
- **Negative parallax**: convergence lines meet in front of the object - object appears closer

## Pictorial Depth Cues (Monocular)

Static cues available even from a single image:

| Cue | Mechanism |
|-----|-----------|
| Linear perspective | Parallel lines converge at vanishing point |
| Texture gradient | Texture density increases with distance |
| Focus and blur | Sharp objects appear closer |
| Atmospheric depth | Distant objects appear hazier |
| Cast shadows | Shadow position indicates depth |
| Occlusion | Closer objects block farther ones |

## Dynamic Depth Cues

Cues that require motion:

- **Motion parallax**: objects at different distances move at different apparent speeds
- **Kinetic depth effect**: rotation reveals 3D structure through horizontal movement
- **Interposition**: dynamic occlusion during movement
- **Highlight movement**: specular reflections shift with viewpoint

> [!IMPORTANT]
> Depth cues are additive and can be combined. Some cues dominate others - for example, binocular disparity is very strong at close range but weak at distance.

## Related Concepts

- [[Human Visual System]]: the biological system processing these cues
- [[Projective Transformation]]: how 3D depth is projected onto 2D
- [[Visual Attention]]: how attention interacts with depth perception
