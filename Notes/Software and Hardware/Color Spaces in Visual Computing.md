---
title: Color Spaces in Visual Computing
aliases:
  - Farbraume
  - Color Models
tags:
  - visual-computing
  - image-processing
description: "Color representation systems used in visual computing including RGB, YCbCr, CIELAB, and perceptual models"
draft: false
---

> [!NOTE] Definition
> Color spaces define mathematical models for representing colors. Different spaces are optimized for different purposes - display, perception, or compression.

## Color Properties

| Property | Description |
|----------|-------------|
| Brightness (Helligkeit) | Overall light intensity |
| Relative brightness | Brightness relative to white |
| Hue (Farbton) | The pure color component |
| Colorfulness (Farbigkeit) | Intensity of the chromatic component |
| Chroma (Buntheit) | Colorfulness relative to white brightness |
| Saturation (Sattigung) | Colorfulness relative to brightness |

### Derived Relationships

$$\text{Chroma} = \frac{\text{Colorfulness}}{\text{Brightness(White)}}$$

$$\text{Relative Brightness} = \frac{\text{Brightness}}{\text{Brightness(White)}}$$

$$\text{Saturation} = \frac{\text{Colorfulness}}{\text{Brightness}} = \frac{\text{Chroma}}{\text{Relative Brightness}}$$

## Technical Color Spaces

- **RGB**: additive, used in displays
- **sRGB**: standardized RGB
- **HSI**: Hue, Saturation, Intensity
- **CMYK**: subtractive, used in printing

## Perceptual Color Spaces

- **YCbCr**: separates luminance (Y) from chrominance (Cb, Cr) - used in [[JPEG Compression]]
- **CIEXYZ**: device-independent reference space
- **CIELAB**: opponent color space, nearly perceptually uniform, models non-linearities of the visual system

## Color Perception Phenomena

- **Metamerism**: two different spectral distributions that produce the same perceived color
  - Observer metamerism: same stimuli, different perception between observers
  - Illuminant metamerism: same reflectance spectra, different appearance under different lighting
- **Simultaneous contrast**: background shifts perceived color
- **Crispening effect**: similar background amplifies perceived color difference

## Color Appearance Models

S-CIELAB and iCAM enable color matching under different viewing conditions.

## Related Concepts

- [[Human Visual System]]: the biological basis for color perception
- [[JPEG Compression]]: uses YCbCr color space
- [[Visual Perception Phenomena]]: contrast and brightness illusions
