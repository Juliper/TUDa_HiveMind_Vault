---
title: Human Visual System
aliases:
  - Das menschliche Auge
  - Visual Perception System
tags:
  - visual-computing
  - human-perception
description: "Structure and function of the human eye including photoreceptors and their distribution"
draft: false
---

> [!NOTE] Definition
> The human visual system captures light through photoreceptors in the retina - rods for contrast/brightness and cones for color - and processes it through multiple neural layers.

## Electromagnetic Radiation

Light is electromagnetic radiation governed by:

$$v \cdot \lambda = c$$

where $v$ is frequency, $\lambda$ is wavelength, and $c$ is the speed of light.

## Photoreceptors

| Receptor | Function | Location | Details |
|----------|----------|----------|---------|
| **Rods** (Stabchen) | Contrast/brightness perception | Outside fovea | Scotopic (night) vision, peak sensitivity at green |
| **Cones** (Zapfen) | Color perception (R, G, B) | Inside fovea | Photopic (day) vision |

### Cone Distribution in the Fovea

- ~10% blue, ~48% green, ~42% red

### Vision Modes

- **Scotopic vision**: night vision using rods, adapted to darkness
- **Photopic vision**: day vision using cones (blue, green, red)

## Bayer Pattern

Photo sensors mimic the receptor distribution of the human eye using the **Bayer matrix** to produce realistic images:
- 50% green, 25% blue, 25% red filters

## Luminance Ranges

The brighter the environment, the more cone vision (color) is used. In darker conditions, rod vision (contrast) dominates.

## Retinal Cell Types

| Cell Type | Function |
|-----------|----------|
| Horizontal cells | Combine receptors from a region |
| Bipolar cells | Filter information |
| Amacrine cells | Temporal processing |
| Ganglion cells | Integrate information |

## Related Concepts

- [[Visual Perception Phenomena]]: illusions and artifacts of the visual system
- [[Weber-Fechner Law]]: quantifying the relationship between stimulus and perception
- [[Depth Cue Theory]]: how the visual system perceives depth
