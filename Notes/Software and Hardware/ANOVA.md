---
title: ANOVA
aliases:
  - Analysis of Variance
  - Varianzanalyse
tags:
  - hci
  - evaluation
  - statistics
description: "A parametric statistical test that compares means across three or more groups or conditions in a single test"
draft: false
---

> [!NOTE] Definition
> ANOVA (Analysis of Variance) is a parametric significance test that determines whether there is a statistically significant difference between the means of three or more groups or conditions, generalizing the [[T-Test]] beyond just two groups.

## Why Not Just Run Multiple T-Tests?

Running a separate t-test for every pair of groups inflates the overall Type I error rate (see the multiple comparisons problem in [[Statistical Significance Testing]]). ANOVA instead tests all groups simultaneously in a single test, controlling the overall error rate, and only if it detects a significant overall difference are pairwise post-hoc tests run to find *which* groups differ.

## Variants

| Variant | Used When |
|---|---|
| **One-way ANOVA** | Comparing 3+ independent groups ([[Between-Subjects and Within-Subjects Design|between-subject design]]) |
| **Repeated-measures ANOVA** | Comparing 3+ related measurements from the same participants ([[Between-Subjects and Within-Subjects Design|within-subject design]]) |

## Assumptions

In addition to the [[T-Test]]'s assumptions (continuous scale, homogeneity of variance, normal distribution), repeated-measures ANOVA additionally assumes **sphericity** - that the variances of the differences between all pairs of conditions are roughly equal.

If assumptions are violated, use the non-parametric alternatives: Kruskal-Wallis (one-way) or Friedman (repeated-measures).

## Related Concepts

- [[T-Test]]: ANOVA generalizes the two-group t-test to three or more groups
- [[Statistical Significance Testing]]: ANOVA is one specific implementation of significance testing, chosen based on study design
- [[Type I and Type II Errors]]: ANOVA controls Type I error inflation compared to running many separate t-tests
