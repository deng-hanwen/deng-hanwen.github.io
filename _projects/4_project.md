---
layout: page
title: Whole-Brain Resting-State fMRI Prediction of Ambiguity Tolerance
description: Connectome-based predictive modelling of resting-state functional connectivity as a predictor of individual differences in ambiguity tolerance
img: assets/img/cpm_thumb.png
importance: 3
category: Computational and Neuroimaging
github: https://github.com/deng-hanwen/RiskBehavior_controlCPM
related_publications: false
---

<p>
  <a href="https://github.com/deng-hanwen/RiskBehavior_controlCPM" class="btn btn-sm z-depth-0" role="button" style="background-color: #424242; color: white;">
    <i class="fab fa-github"></i> View Code on GitHub
  </a>
</p>

*Hanwen Deng, Francesca M. LoFaro, Steven Riley, Sarah W. Yip, Anna B. Konova*

*Yale University & Rutgers University. Supervised by Dr Sarah Yip & Dr Anna Konova.*

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

CPM (Finn et al., 2015; Shen et al., 2017) is a data-driven approach that uses whole-brain functional connectivity matrices to predict individual differences in behaviour. Rather than selecting regions of interest a priori, CPM identifies edges — pairwise correlations between brain nodes — whose strength across participants covaries with the behavioural target, then uses those edges to predict behaviour in held-out individuals.

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/cpm_schematic.png" alt="Schematic diagram of CPM pipeline showing feature selection, edge summation, model fitting, and prediction" style="max-width: 95%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 1.</em> CPM pipeline. (A) Edges in each subject's FC matrix are correlated with the behavioural target across participants to select positive and negative predictive networks. (B) Selected edge weights are summed per subject into network strength scores. (C) A linear brain–behaviour model is fit on training data. (D) The model is applied to held-out subjects' FC matrices to generate behavioural predictions. Reproduced from Yip et al. (2019).</p>
</div>

The pipeline applied here:

1. Correlate each edge in the connectivity matrix with the behavioural target (γ, α, or β) across subjects
2. Select edges at *p* < 0.01 into positive and negative networks
3. Sum selected edges into network strength scores per subject
4. Predict held-out subjects via leave-one-out cross-validation (LOO-CV)
5. Evaluate prediction accuracy as the Pearson correlation between predicted and observed behaviour

CPM was applied to resting-state fMRI connectivity matrices derived from the **268-node Shen atlas** (27P noise model), and run separately for γ, α, and β.

---

## Key Findings

Resting-state FC did not significantly predict ambiguity tolerance, risk tolerance, or choice sensitivity under cross-validation. None of the CPM models achieved above-chance prediction accuracy.

This null result is interpretable in the context of accumulating evidence that **state-dependent processes** — engaged specifically during task performance — may be necessary to capture individual differences in decision-making parameters that are context-sensitive. Resting-state connectivity, reflecting intrinsic brain organisation in the absence of task demands, may be insufficient to capture the variance in ambiguity tolerance that is sensitive to contextual and attentional factors.

The findings directly inform future study design: **task-based fMRI paradigms** that engage ambiguity processing during scanning are likely to offer greater predictive power than resting-state approaches for this class of decision-making phenotype.

Taken together with the companion clinical study — where γ also failed to predict prospective drug use in an OUD sample — a coherent picture emerges: **ambiguity tolerance as measured by this paradigm may be more state-dependent than a stable individual trait**, sensitive to clinical context, cognitive state, and task engagement rather than reflecting fixed neural architecture accessible from resting-state connectivity alone. This has direct implications for the design of computational psychiatry studies that aim to use decision-making parameters as translational biomarkers.

---

## Code & Reproducibility

All analysis code is available at **[github.com/deng-hanwen/RiskBehavior_controlCPM](https://github.com/deng-hanwen/RiskBehavior_controlCPM)**, including MATLAB scripts for behavioural preprocessing, utility model fitting, and the CPM pipeline. Raw data are not shared to protect participant confidentiality.

---

## References

Finn, E. S., Shen, X., Scheinost, D., Rosenberg, M. D., Chun, M., Papademetris, X., … Constable, R. T. (2015). Functional connectome fingerprinting: Identifying individuals using patterns of brain connectivity. *Nature Neuroscience, 18*(11), 1664–1671.

Shen, X., Finn, E. S., Scheinost, D., Rosenberg, M. D., Chun, M. M., Papademetris, X., & Constable, R. T. (2017). Using connectome-based predictive modeling to predict individual behavior from brain connectivity. *Nature Protocols, 12*(3), 506–518.

Yip, S. W., Scheinost, D., Potenza, M. N., & Carroll, K. M. (2019). Connectome-based prediction of cocaine abstinence. *American Journal of Psychiatry, 176*(2), 156–164.
