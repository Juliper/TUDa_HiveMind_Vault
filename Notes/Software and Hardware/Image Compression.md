---
title: Image Compression
aliases:
  - Bildkompression
tags:
  - visual-computing
  - image-processing
description: "Techniques for reducing image data size through lossless or lossy compression methods"
draft: false
---

> [!NOTE] Definition
> Image compression reduces the amount of data needed to represent an image. Rasterization and sampling of light intensity functions produces enormous data volumes, making compression essential.

## Lossless Compression

Encodes data without any information loss - only redundancy is removed. The original image can be perfectly reconstructed.

| Method | Description |
|--------|-------------|
| Variable-Length Coding | Shorter codes for frequent values (e.g., Huffman) |
| Bit-Plane Coding | Encoding individual bit planes separately |
| Predictive Coding | Encoding prediction errors instead of raw values |
| Lempel-Ziv-Welch | Dictionary-based compression of repeated patterns |

## Lossy Compression

Encodes data with controlled information loss, discarding imperceptible differences to achieve higher compression ratios.

## Related Concepts

- [[JPEG Compression]]: the most widely used lossy image compression standard
- [[Signal Sampling and Aliasing]]: sampling as the first step producing raw image data
- [[Image Histogram]]: understanding data distribution for effective compression
