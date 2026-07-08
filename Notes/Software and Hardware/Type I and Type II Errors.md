---
title: Type I and Type II Errors
aliases:
  - Statistical Errors
  - Alpha und Beta Fehler
tags:
  - hci
  - evaluation
  - statistics
description: "The two ways a significance test's decision about the null hypothesis can be wrong - a false positive or a false negative"
draft: false
---

> [!NOTE] Definition
> A Type I error is rejecting a true null hypothesis (a false positive); a Type II error is failing to reject a false null hypothesis (a false negative).

## The Two Errors

| | H0 is actually True | H0 is actually False |
|---|---|---|
| **Reject H0** | Type I Error (false positive), probability $\alpha$ | Correct decision |
| **Fail to reject H0** | Correct decision | Type II Error (false negative), probability $\beta$ |

## Court Hearing Analogy

Treating H0 as "the defendant is innocent":
- **Type I error**: convicting an innocent defendant (concluding an effect exists when it doesn't)
- **Type II error**: acquitting a guilty defendant (missing a real effect that does exist)

## Tradeoffs

Lowering the significance threshold $\alpha$ (e.g., from 0.05 to 0.01) reduces the Type I error rate but increases the Type II error rate for a fixed sample size, since the test becomes more conservative. The only way to reduce both simultaneously is to increase [[Sample Size and Statistical Power|sample size]] or effect size.

> [!IMPORTANT]
> Running many significance tests without correction (see the multiple comparisons problem in [[Statistical Significance Testing]]) directly increases the overall Type I error rate across the set of tests.

## Related Concepts

- [[Statistical Significance Testing]]: defines $\alpha$, the accepted Type I error rate
- [[Sample Size and Statistical Power]]: an underpowered study has an elevated Type II error rate
- [[T-Test]] and [[ANOVA]]: any significance test carries both error risks
