---
title: T-Test
aliases:
  - Student's t-test
  - t-Test
tags:
  - hci
  - evaluation
  - statistics
description: "A parametric statistical test that compares the means of two groups to determine if their difference is statistically significant"
draft: false
---

> [!NOTE] Definition
> A t-test is a parametric significance test that compares the means of two groups (or two conditions) and computes a p-value for the probability that the observed difference occurred by chance under the null hypothesis of equal means.

## Variants

| Variant | Used When |
|---|---|
| **Independent samples t-test** | Comparing two separate groups ([[Between-Subjects and Within-Subjects Design|between-subject design]]) |
| **Paired samples t-test** | Comparing two related measurements from the same participants ([[Between-Subjects and Within-Subjects Design|within-subject design]]) |

## Assumptions

A t-test is only valid when:
1. The dependent variable is measured on a **continuous scale** (interval or ratio, see [[Data Types in Quantitative Research]])
2. **Homogeneity of variance** - the two groups have approximately equal variance
3. The data is (approximately) **normally distributed**

If these assumptions are violated, a non-parametric alternative such as Mann-Whitney U (independent) or Wilcoxon signed-rank (paired) should be used instead - see [[Statistical Significance Testing]].

## Worked Example

Comparing task completion time between two input devices (mouse vs. touch), each tested by a separate group of participants:

1. Compute the mean and standard deviation of completion time for each group (see [[Descriptive Statistics]])
2. Check that variances are roughly equal and data is roughly normal
3. Run an independent samples t-test on the two groups' completion times
4. If $p \leq 0.05$, conclude the input devices produce significantly different completion times

## Related Concepts

- [[Statistical Significance Testing]]: t-tests are one specific implementation of significance testing
- [[ANOVA]]: the generalization of the t-test to three or more groups
- [[Data Types in Quantitative Research]]: t-tests require interval or ratio data
- [[Between-Subjects and Within-Subjects Design]]: determines whether an independent or paired t-test applies
