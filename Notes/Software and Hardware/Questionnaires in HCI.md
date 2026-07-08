---
title: Questionnaires in HCI
aliases:
  - Likert Scale
  - NASA-TLX
  - SUS
  - Fragebögen
tags:
  - hci
  - evaluation
  - research-methods
description: "Standardized and custom rating instruments used to quantify subjective factors like usability, workload, and satisfaction"
draft: false
---

> [!NOTE] Definition
> Questionnaires are instruments that help quantify subjective factors, such as ease-of-use, fun, or fatigue, by having participants rate statements on a defined scale, complementing objective data collected through logging or measurement.

## Objective Data vs. Subjective Factors

In real experiments, both are usually collected simultaneously: **during** a condition, objective data is logged automatically (e.g., time needed for completion, accuracy); **after** a condition, participants fill in a questionnaire to capture subjective perception (e.g., NASA-TLX, SUS, a presence questionnaire). Subjective factors can still be captured quantitatively, e.g., rating perceived pain on a Likert scale.

## Rating Scales

Questionnaire responses are measured on a rating scale, which can be as simple as yes/no, an ordered set like *very low, low, high*, a Likert scale, or a fully custom scale.

## Likert Scale

Named after Rensis Likert. Rather than asking direct questions, a Likert scale measures the participant's **agreement** with a series of statements, typically ranging from *strongly disagree* to *strongly agree* in 5 or 7 steps with a neutral midpoint.

> [!IMPORTANT]
> A variant with an **even** number of options removes the neutral midpoint, forcing participants to commit to either a positive or negative tendency.

## Standardized Questionnaires

| Questionnaire | Measures |
|---|---|
| **NASA-TLX** | Perceived task workload (mental, physical, temporal demand, performance, effort, frustration) |
| **SUS** (System Usability Scale) | General perceived usability of a system |
| **Presence Questionnaire** | Sense of presence/immersion, common in VR research |

## Standardized vs. Custom Questionnaires

Whenever a standardized questionnaire exists for the factor being measured, **use it** - it is validated and enables comparison across studies. When no exact match exists, look for a questionnaire that measured a similar factor and use it or draw inspiration from it, rather than designing an entirely custom questionnaire from scratch, since custom questionnaires risk unvalidated wording, biased phrasing, and results that cannot be compared to prior work.

## Related Concepts

- [[Controlled Experiment]]: questionnaires are collected as part of the "Measures" stage of a study
- [[Data Types in Quantitative Research]]: Likert-scale data is typically treated as ordinal
- [[Hawthorne Effect]]: self-report questionnaires are also susceptible to participants answering in a socially desirable way
