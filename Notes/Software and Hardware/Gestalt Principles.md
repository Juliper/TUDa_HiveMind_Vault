---
title: Gestalt Principles
aliases:
  - Gestaltgesetze
  - Gestalt Laws of Perception
tags:
  - hci
  - perception
  - visual-design
description: "Perceptual organization laws describing how humans group visual elements into coherent wholes"
draft: false
---

Gestalt Principles are a set of laws from perceptual psychology that describe how humans naturally organize visual elements into groups and coherent patterns. In HCI, they are fundamental for designing interfaces that users can parse quickly and correctly.

The core idea: the brain does not perceive individual elements in isolation but actively structures them into meaningful wholes ("Gestalten").

## Key Principles

### Proximity

Elements that are close together are perceived as belonging to the same group. In UI design, spacing is the primary tool for indicating which controls or labels belong together.

### Similarity

Elements that share visual properties (color, shape, size, orientation) are perceived as related. For example, all clickable links sharing the same blue color signals they are the same type of element.

### Continuity

The eye follows smooth paths. Elements arranged along a line or curve are perceived as more related than elements not on the path. This guides layout of navigation bars, timelines, and flows.

### Closure

The brain completes incomplete shapes. A circle with a gap is still perceived as a circle. This allows designers to use minimal visual elements — users fill in the rest.

### Common Region

Elements within the same bounded area (border, background color) are perceived as a group. Cards, panels, and dialog boxes leverage this principle.

### Figure-Ground

The brain separates a scene into a foreground object (figure) and background. Modal dialogs use this by dimming the background to establish the dialog as the figure.

### Connectedness

Elements connected by lines or other visual links are perceived as related, even more strongly than proximity. Used in flowcharts, node-link diagrams, and Mermaid graphs.

### Common Fate

Elements that move in the same direction or at the same speed are perceived as a cohesive unit rather than individual components. In UI design, this principle is realized through animation - elements that animate together are read as belonging together.

## Example

A form with fields for "Name" and "Email" grouped close together (proximity) with a visible border around them (common region) signals they belong to the same section ("Personal Info"), even without an explicit label.

## Application in Interface Design

| Principle | UI Application |
|---|---|
| Proximity | Grouping form fields, toolbar sections |
| Similarity | Consistent button styles, link colors |
| Continuity | Navigation bars, progress indicators |
| Closure | Loading spinners, icon design |
| Common Region | Cards, grouped settings panels |
| Figure-Ground | Modal overlays, focus states |
| Common Fate | Animations, coordinated motion of related elements |

## Related Concepts

- [[Cognitive Load Theory]]: Gestalt grouping reduces cognitive load by pre-structuring information
- [[Mental Models]]: well-designed Gestalt grouping aligns with users' expectations
- [[Dark Patterns]]: Gestalt principles are sometimes exploited via Interface Interference to mislead users
