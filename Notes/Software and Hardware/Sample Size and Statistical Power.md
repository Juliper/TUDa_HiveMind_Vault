---
title: Sample Size and Statistical Power
aliases:
  - Stichprobengröße
  - G*Power
tags:
  - hci
  - evaluation
  - research-methods
description: "How many participants an experiment needs to reliably detect a real effect without being needlessly expensive to run"
draft: false
---

> [!NOTE] Definition
> Sample size planning determines how many participants are needed so that a study has enough statistical power to detect a real effect (if one exists) while avoiding wasted effort recruiting more participants than necessary.

## Underpowered vs. Overpowered Studies

- An **underpowered** study has too few participants: a real effect may fail to reach statistical significance simply because the sample was too small, producing a false negative.
- An **overpowered** study has more participants than needed: it wastes time and resources, and can make even trivially small, practically meaningless effects appear "statistically significant."

## Determining Sample Size

Tools such as **G*Power** compute the required sample size ahead of time from the expected effect size, desired significance level (commonly $\alpha = 0.05$), and desired statistical power (commonly $1 - \beta = 0.8$, i.e., an 80% chance of detecting a true effect).

## Sampling and Population Inference

A study samples a subset of the target population and uses statistical inference to generalize findings back to that population. The sample must be reasonably representative for this generalization to hold - see [[Control, Random, and Confounding Variables]] for how uncontrolled sampling bias can undermine this.

## Related Concepts

- [[Statistical Significance Testing]]: sample size directly affects the ability to detect significant effects
- [[Type I and Type II Errors]]: underpowered studies increase the risk of a Type II error (false negative)
- [[Controlled Experiment]]: sample size planning is part of designing a lab experiment
