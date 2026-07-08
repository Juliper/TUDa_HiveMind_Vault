---
title: Controlled Experiment
aliases:
  - Kontrolliertes Experiment
tags:
  - hci
  - evaluation
  - research-methods
description: "A quantitative study design that manipulates independent variables to measure their causal effect on dependent variables while holding other factors constant"
draft: false
---

> [!NOTE] Definition
> A controlled experiment is a quantitative evaluation method in which the researcher deliberately manipulates one or more independent variables and measures their effect on dependent variables, while controlling other factors, in order to establish a causal relationship.

## The Underlying Model

A controlled experiment assumes the measured outcome can be modeled as:

$$Y = f(X) + \varepsilon$$

where $Y$ is the dependent variable, $X$ represents the manipulated independent variable(s), $f$ is the (unknown) true relationship the experiment tries to uncover, and $\varepsilon$ is noise from unknown or uncontrolled variables. The goal of good experimental design is to make $\varepsilon$ as small and as unbiased as possible so that the estimated effect of $X$ on $Y$ is trustworthy.

## Quantitative Evaluation Formats

| Format | Precision | Realism | Generalizability | Obtrusiveness |
|---|---|---|---|---|
| **Lab Experiment** | High | Low | Low | Obtrusive |
| **Field Study** | Low | High | High | Can be unobtrusive |
| **Survey** | Medium | Medium | High (large N) | Unobtrusive |

- **Precision**: how tightly controlled and measurable the conditions are
- **Realism**: how closely the setting resembles real-world use
- **Generalizability**: how well findings transfer to the broader population
- **Obtrusiveness**: how much the study setup itself changes participant behavior

There is an inherent tradeoff: lab experiments maximize precision at the cost of realism, field studies maximize realism at the cost of precision, and no single format maximizes all four properties simultaneously.

## Designing a Lab Experiment

1. Formulate a hypothesis with clear [[Independent and Dependent Variables]]
2. Decide on [[Between-Subjects and Within-Subjects Design|within- or between-subjects design]]
3. Recruit a representative sample of users (see [[Sample Size and Statistical Power]])
4. Control ordering effects via [[Counterbalancing]]
5. Standardize hardware, environment, and instructions across all participants
6. Collect data via logging and/or [[Questionnaires in HCI|questionnaires]]

## Related Concepts

- [[Independent and Dependent Variables]]: the core variables manipulated and measured
- [[Control, Random, and Confounding Variables]]: the other variables that must be accounted for
- [[Validity and Reliability]]: the two properties a well-designed experiment must have
- [[Research Question and Hypothesis Formulation]]: the starting point before designing an experiment
- [[Between-Subjects and Within-Subjects Design]]: the two main ways to assign participants to conditions
