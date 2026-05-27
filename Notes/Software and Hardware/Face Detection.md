---
title: Face Detection
aliases:
  - Gesichtsdetektion
  - Gesichtserkennung
tags:
  - visual-computing
  - computer-vision
description: "Detecting and recognizing faces in images using object representation, training data, and classifiers"
draft: false
---

> [!NOTE] Definition
> Face detection is the task of locating and identifying faces in images, requiring an object representation, training data, and a classification method.

## Key Aspects

### Object Representation
- **Local features**: individual facial features (eyes, nose, mouth)
- **Global arrangement**: spatial relationships between features

### Training Data
- **Positive examples**: images containing faces
- **Negative examples**: images without faces

### Classifier and Learning Method
A trained model that separates face from non-face regions.

## Appearance Model Pipeline

```mermaid
flowchart LR
    A[Object Representation<br>local/global features] --> B[Training Data<br>positive + negative] --> C[Classifier<br>learning method]
```

## Recognition Types

| Type | Description |
|------|-------------|
| **Verification** | Does a given feature match an entry in the database? |
| **Identification** | Determine which person the features belong to |

## Related Concepts

- [[Bayes Decision Theory in Computer Vision]]: probabilistic classification framework
- [[Visual Computing Overview]]: face detection as a key visual computing application
