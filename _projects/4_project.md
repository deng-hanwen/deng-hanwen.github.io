---
layout: page
title: Whole-Brain Resting-State fMRI Prediction of Ambiguity Tolerance
description: Connectome-based predictive modelling of resting-state functional connectivity as a predictor of individual differences in ambiguity tolerance
img: assets/img/7.jpg
importance: 3
category: research
github: https://github.com/deng-hanwen/RiskBehavior_controlCPM
related_publications: false
---

<p>
  <a href="https://github.com/deng-hanwen/RiskBehavior_controlCPM" class="btn btn-sm z-depth-0" role="button" style="background-color: #424242; color: white;">
    <i class="fab fa-github"></i> View Code on GitHub
  </a>
</p>

> **Note:** Accepted as Poster Presentation at the Computational Psychiatry Conference, 2026.

---

## Overview

Individual differences in how people tolerate ambiguous outcomes — situations where probabilities are unknown — have been linked to a range of psychiatric conditions, including anxiety, addiction, and mood disorders. Yet the neural basis of **ambiguity tolerance** at the individual level remains poorly characterised.

This project asks whether **resting-state functional connectivity** can predict individual differences in ambiguity tolerance in a healthy community sample (n = 59), using connectome-based predictive modelling (CPM) — a data-driven framework that identifies brain–behaviour associations at the whole-connectome level without requiring a priori region-of-interest selection.

This study is conceptually linked to a companion clinical project — [Computational Markers and Clinical Vulnerability in Early OUD Treatment](/projects/3_project/) — in which ambiguity tolerance (γ) was extracted from the same decision-making paradigm in an OUD sample, but did not predict prospective opioid use. The null clinical result raised the question of whether γ reflects a stable neural trait at all, motivating the current investigation of its neural basis in a healthy population.

---

## Methods

### Behavioural Parameters

Participants completed the **Lottery and Sure-thing Risk and Ambiguity (LSRA) task** — an incentivised economic decision-making paradigm in which they chose between a guaranteed payoff and lotteries varying in risk (known probabilities) and ambiguity (unknown probabilities).

Choices were fitted with an expected utility model to extract three parameters per participant:

| Parameter | Interpretation |
|---|---|
| **γ (gamma)** | Ambiguity tolerance — willingness to engage with unknown-probability outcomes |
| **α (alpha)** | Risk tolerance — curvature of the utility function |
| **β (beta)** | Choice sensitivity (inverse temperature) |

Model quality was assessed via *R*² ≥ 0.10 and parameter bound checks. Final sample after QC: n = 59.

### Connectome-Based Predictive Modelling (CPM)

CPM was applied to resting-state fMRI connectivity matrices derived from the **268-node Shen atlas** (27P noise model). The pipeline:

1. Correlate each edge in the connectivity matrix with the behavioural target across subjects
2. Select edges at *p* < 0.01 into positive and negative networks
3. Sum selected edges into network strength scores per subject
4. Predict held-out subjects via leave-one-out cross-validation (LOO-CV)
5. Evaluate prediction accuracy as the correlation between predicted and observed behaviour

CPM was run separately for γ, α, and β.

---

## Key Findings

Resting-state FC did not significantly predict ambiguity tolerance, risk tolerance, or choice sensitivity under cross-validation. None of the CPM models achieved above-chance prediction accuracy.

This null result is interpretable in the context of accumulating evidence that **state-dependent processes** — engaged specifically during task performance — may be necessary to capture individual differences in decision-making parameters that are context-sensitive. Resting-state connectivity, reflecting intrinsic brain organisation in the absence of task demands, may be insufficient to capture the variance in ambiguity tolerance that is sensitive to contextual and attentional factors.

The findings directly inform future study design: **task-based fMRI paradigms** that engage ambiguity processing during scanning are likely to offer greater predictive power than resting-state approaches for this class of decision-making phenotype.

Taken together with the companion clinical study — where γ also failed to predict prospective drug use in an OUD sample — a coherent picture emerges: **ambiguity tolerance as measured by this paradigm may be more state-dependent than a stable individual trait**, sensitive to clinical context, cognitive state, and task engagement rather than reflecting fixed neural architecture accessible from resting-state connectivity alone. This has direct implications for the design of computational psychiatry studies that aim to use decision-making parameters as translational biomarkers.

---

## Code & Reproducibility

All analysis code is available at **[github.com/deng-hanwen/RiskBehavior_controlCPM](https://github.com/deng-hanwen/RiskBehavior_controlCPM)**, including MATLAB scripts for behavioural preprocessing, utility model fitting, and the CPM pipeline. Raw data are not shared to protect participant confidentiality.

*Yale University & Rutgers University. Dr Sarah Yip & Dr Anna Konova.*
