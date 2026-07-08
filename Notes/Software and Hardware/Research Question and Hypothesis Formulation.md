---
title: Research Question and Hypothesis Formulation
aliases:
  - Null Hypothesis
  - Forschungsfrage und Hypothese
tags:
  - hci
  - evaluation
  - research-methods
description: "How a good research question is scoped and translated into a testable hypothesis and its null hypothesis before running an experiment"
draft: false
---

> [!NOTE] Definition
> A research question is an open-ended question that frames what a study aims to learn; a hypothesis is a concrete, testable claim derived from that question predicting the outcome of an experiment, stated alongside its null hypothesis (H0) - the claim of no effect that the experiment tries to statistically reject.

## The Research Pipeline

```mermaid
flowchart LR
    A[Idea] --> B[Research Question]
    B --> C[Hypotheses]
    C --> D[Study Design]
    D --> E[Measures]
```

## Checklist for a Good Research Question

1. Is it open-ended (not answerable with a simple yes/no)?
2. Is it appropriate in scope - focused and narrow enough for the project?
3. Does it suggest factors that can actually be measured?
4. Is it relevant to the intended audience?
5. Is answering it manageable, with access to enough data or participants?
6. Is the topic genuinely of interest?

> [!IMPORTANT]
> Starting a research question with **"How"** is usually a solid starting point, and it is fine to explicitly reference the independent and dependent variables within the question itself.

## From Research Question to Hypothesis

A hypothesis must be a **precise, testable statement**, not just a restatement of the research question, and should clearly name both the independent and dependent variable.

**Example**:
- Research question: *"Which input device allows the user to perform best in competitive third-person games?"*
- Hypothesis: *"Participants will receive higher scores using mouse input compared to touch and controller input when playing X minutes of Game Y."*

## Null Hypothesis (H0)

The null hypothesis is a term from statistical testing stating that the samples being compared are drawn from the **same underlying statistical distribution** - i.e., that the independent variable has **no effect** on the dependent variable. An experiment's goal is to gather enough statistical evidence to **reject H0** in favor of the alternative (research) hypothesis; see [[Statistical Significance Testing]] for how this rejection decision is made.

## Related Concepts

- [[Controlled Experiment]]: hypotheses are what a controlled experiment is designed to test
- [[Independent and Dependent Variables]]: both must be explicitly named in a well-formed hypothesis
- [[Statistical Significance Testing]]: the mechanism used to accept or reject H0 based on collected data
