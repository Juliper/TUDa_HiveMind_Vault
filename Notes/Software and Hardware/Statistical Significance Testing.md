---
title: Statistical Significance Testing
aliases:
  - p-value
  - Bonferroni Correction
  - Signifikanztest
tags:
  - hci
  - evaluation
  - statistics
description: "The process of deciding whether an observed effect is unlikely to have occurred by chance, using p-values to reject or fail to reject the null hypothesis"
draft: false
---

> [!NOTE] Definition
> Statistical significance testing evaluates whether the data provides enough evidence to reject the [[Research Question and Hypothesis Formulation|null hypothesis (H0)]], by computing a p-value that estimates the probability of observing results at least as extreme as the actual data, assuming H0 were true.

## The p-value Logic

- Choose a significance threshold $\alpha$ in advance, conventionally $\alpha = 0.05$
- If the computed $p \leq \alpha$, reject H0: the observed effect is unlikely to be due to chance alone, supporting the alternative hypothesis
- If $p > \alpha$, fail to reject H0: there is not enough evidence of a real effect (this does **not** prove H0 is true)

## Choosing the Right Test

The correct statistical test depends on the study design and the [[Data Types in Quantitative Research|data type]] of the dependent variable:

| Design | Parametric (interval/ratio, normal) | Non-parametric (ordinal or non-normal) |
|---|---|---|
| Two independent groups | [[T-Test|Independent t-test]] | Mann-Whitney U |
| Two related measures (within-subject) | [[T-Test|Paired t-test]] | Wilcoxon signed-rank |
| 3+ independent groups | One-way [[ANOVA]] | Kruskal-Wallis |
| 3+ related measures | Repeated-measures [[ANOVA]] | Friedman |

## The Multiple Comparisons Problem

Running many significance tests on the same dataset inflates the chance of a false positive: with $\alpha = 0.05$, each additional test carries its own 5% chance of a spurious "significant" result, so testing many comparisons makes at least one false positive increasingly likely (**alpha inflation**). This risk is exactly a [[Type I and Type II Errors|Type I error]] compounding across tests.

**Bonferroni correction** counters this by dividing the significance threshold by the number of comparisons $m$:

$$\alpha_{corrected} = \frac{\alpha}{m}$$

so each individual test must clear a stricter bar before being called significant.

## Related Concepts

- [[Research Question and Hypothesis Formulation]]: defines the H0 that significance testing evaluates
- [[Type I and Type II Errors]]: the two ways a significance test decision can be wrong
- [[T-Test]] and [[ANOVA]]: the two most common parametric significance tests in HCI experiments
- [[Sample Size and Statistical Power]]: affects the ability of a test to detect a true effect
