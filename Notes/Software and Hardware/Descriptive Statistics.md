---
title: Descriptive Statistics
aliases:
  - Deskriptive Statistik
tags:
  - hci
  - evaluation
  - statistics
description: "Summary measures - mean, median, mode, variance, standard deviation, and interquartile range - used to characterize a dataset before inferential testing"
draft: false
---

> [!NOTE] Definition
> Descriptive statistics summarize the central tendency and spread of a dataset, providing a first, simple characterization of the data before any inferential (significance) testing is performed.

## Central Tendency

| Measure | Description |
|---|---|
| **Mean** | The arithmetic average; sensitive to outliers |
| **Median** | The middle value when sorted; robust to outliers |
| **Mode** | The most frequently occurring value; the only central tendency measure valid for nominal data |

## Spread / Dispersion

| Measure | Description |
|---|---|
| **Variance** | Average squared deviation from the mean |
| **Standard Deviation (SD)** | Square root of the variance, in the same units as the data |
| **Interquartile Range (IQR)** | Range between the 25th and 75th percentile; robust to outliers |
| **Median Absolute Deviation (MAD)** | Median of the absolute deviations from the median; a robust alternative to SD |

> [!IMPORTANT]
> Which measures are valid depends on the [[Data Types in Quantitative Research|data's measurement scale]]: mode works for nominal data, median and IQR require at least ordinal data, and mean, variance, and SD require interval or ratio data.

## Role in the Analysis Pipeline

Descriptive statistics are typically computed first to get an intuitive feel for the data (e.g., "on average, condition A was faster than condition B"), before [[Statistical Significance Testing]] determines whether that difference is unlikely to have occurred by chance.

## Related Concepts

- [[Data Types in Quantitative Research]]: determines which descriptive measures are mathematically valid
- [[Statistical Significance Testing]]: the next step after describing the data, to test whether observed differences are meaningful
- [[T-Test]]: a common significance test that builds on the mean and standard deviation of two groups
