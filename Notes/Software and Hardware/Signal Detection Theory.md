---
title: Signal Detection Theory
aliases:
  - SDT
  - Signalentdeckungstheorie
tags:
  - hci
  - perception
  - decision-making
description: "A framework for analyzing how humans distinguish meaningful signals from noise under uncertainty"
draft: false
---

Signal Detection Theory (SDT) is a statistical framework originally from psychophysics (Tanner & Swets, 1954) that models how humans (and systems) distinguish meaningful stimuli (signals) from background noise. In HCI, SDT is used to analyze notification design, alarm systems, search result evaluation, and any scenario where users must make detection judgments under uncertainty.

## The Decision Matrix

Every detection decision has four possible outcomes:

|  | Signal Present | Signal Absent |
|---|---|---|
| **User says "yes"** | **Hit** (true positive) | **False Alarm** (false positive) |
| **User says "no"** | **Miss** (false negative) | **Correct Rejection** (true negative) |

## Key Concepts

### Sensitivity ($d'$)

$d'$ (d-prime) measures the observer's ability to discriminate signal from noise — the distance between the signal and noise distributions:

$$d' = z(\text{Hit Rate}) - z(\text{False Alarm Rate})$$

Higher $d'$ = better discrimination. A $d'$ of 0 means the observer is guessing.

### Response Bias ($\beta$ or criterion $c$)

The threshold the observer sets for saying "yes." A **liberal criterion** (low threshold) produces more hits but also more false alarms. A **conservative criterion** (high threshold) reduces false alarms but increases misses.

The optimal criterion depends on the **costs and payoffs** of each outcome.

## Application in HCI

| Scenario | Signal | Design Consideration |
|---|---|---|
| Email spam filter | Spam email | Low miss rate (catch all spam) vs. low false alarm rate (don't filter real mail) |
| Medical alert system | Critical patient event | Extremely costly misses → liberal criterion, accept more false alarms |
| Notification system | Important notification | Too many false alarms → users habituate and ignore all notifications ("alarm fatigue") |
| Search engine results | Relevant result | Balance precision (few false alarms) and recall (few misses) |

## Example

A hospital monitor that beeps for abnormal heart rhythms. If sensitivity ($d'$) is low, staff cannot distinguish real events from artifacts. If the criterion is too liberal, constant false alarms lead to **alarm fatigue** — staff start ignoring all alarms, including real ones. Good design increases $d'$ through better sensors and adjusts the criterion based on clinical costs.

## Related Concepts

- [[Fitts's Law]]: both model human performance tradeoffs (speed-accuracy vs. sensitivity-bias)
- [[Human Error in HCI]]: misses and false alarms are systematic error types explained by SDT
