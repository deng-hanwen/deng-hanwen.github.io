---
layout: page
title: Computational Markers and Clinical Vulnerability in Early OUD Treatment
description: MRes dissertation — utility-based computational modelling of a risk and ambiguity decision-making task in methadone treatment, with propensity score correction for non-random missingness
img: assets/img/oud_thumb.png
importance: 2
category: Computational and Neuroimaging
github: https://github.com/deng-hanwen/OUD_ambiguity_tolerance
related_publications: false
---

<p>
  <a href="https://github.com/deng-hanwen/OUD_ambiguity_tolerance" class="btn btn-sm z-depth-0" role="button" style="background-color: #424242; color: white;">
    <i class="fab fa-github"></i> View Code on GitHub
  </a>
</p>

> **Note:** MRes Dissertation — Distinction. Accepted for Rapid Fire Oral Presentation at APA Division 12 Annual Conference, 2026.

---

## Overview

A central goal of computational psychiatry is to extract latent decision-making parameters from behaviour that index clinical vulnerability — and to use these as prospective biomarkers in treatment contexts. This dissertation project applies that framework to early opioid use disorder (OUD) treatment, asking whether **ambiguity tolerance** — a computationally derived measure of willingness to engage with outcomes of unknown probability — predicts prospective opioid use in individuals initiating methadone treatment (MOUD).

The study uses a dense longitudinal design: 15 participants completed a Risk and Ambiguity Decision-Making Task across up to 8 weekly sessions, alongside urine toxicology screening (UTOX) and comprehensive clinical assessments. A secondary question emerged from the data itself: **34.5% of planned sessions were excluded** for poor behavioural quality. Rather than treating this as nuisance, the project investigates whether exclusion patterns carry clinical signal — and corrects for the resulting bias.

---

## Study Design

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/oud_study_design.png" alt="Study design: 16 subjects tracked over 8 weeks of MOUD" style="max-width: 90%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 1.</em> Longitudinal design: participants accepted onto Medications for Opioid Use Disorder (MOUD) completed behavioural assessments and urine toxicology screening across up to 8 weekly sessions. Adapted from iStock (2024).</p>
</div>

---

## Task: Risk and Ambiguity Decision-Making

Participants completed a 120-trial decision-making task (Konova et al., 2020) presented as two interleaved contexts:

- **Known-risk context (60 trials):** Choices between a safe option and a lottery with known probability (*p* = 25%, 50%, or 75%) and reward value (*v* = $5–$66)
- **Ambiguity context (60 trials):** Choices with partially obscured probabilities (ambiguity level *A* = low, medium, or high), requiring subjects to form subjective probability estimates

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/oud_task.png" alt="Risk and Ambiguity Task design showing trial structure" style="max-width: 95%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 2.</em> Risk and Ambiguity Task structure. Left: known-risk context with three probability levels. Right: ambiguity context with partially occluded probability bars. Panel A shows a representative trial sequence: decision screen (3 s), response (1.5 s), feedback (0.5 s), ITI (0.5–1.5 s). Reproduced from Konova et al. (2020).</p>
</div>

---

## Computational Model

Choices were modelled using an **expected utility framework** adapted from Konova et al. (2020), with three free parameters:

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/oud_model.png" alt="Computational model: utility equation and probabilistic choice rule" style="max-width: 90%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 3.</em> Computational model. Top: utility equation for the lottery option, where <em>p</em> is the known risk probability, <em>β</em> scales the ambiguity adjustment (higher β = greater ambiguity aversion), <em>A</em> is ambiguity level, and α is the risk tolerance (curvature of the utility function). Bottom: softmax decision rule. Reproduced from Konova et al. (2020).</p>
</div>

The three free parameters are:

| Parameter | Name | Interpretation |
|-----------|------|----------------|
| **α (alpha)** | Risk tolerance | Curvature of utility over outcomes; α < 1 = risk aversion |
| **γ (gamma)** | Ambiguity tolerance | Subjective adjustment of ambiguous probabilities; higher = more willing to engage with uncertainty |
| **μ (mu)** | Choice sensitivity | Inverse temperature of the softmax; lower = noisier choices |

Parameters were estimated per session via maximum likelihood estimation. Inclusion required *R*² ≥ 0.10 and parameter bounds checks on α and μ.

---

## Data Quality and Missingness

### Session Inclusion Heatmap

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/oud_fig2_inclusion.png" alt="Session inclusion heatmap: blue=included, red=excluded, grey=missing" style="max-width: 80%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 4.</em> Participant session inclusion status across the 8-week protocol. Blue cells (✓) indicate sessions included in analysis; red cells (✗) indicate sessions excluded due to poor behavioural quality (R² < 0.10 or parameter bounds violations); grey cells indicate missing sessions.</p>
</div>

Exclusion was not random: UTOX-positive sessions were **6.8× more likely** to be excluded, revealing that data quality itself indexes active substance use. This motivated two additional analyses beyond the primary research question.

### Clinical Predictors of Data Quality

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/oud_fig5_cliffs.png" alt="Cliff's delta bar chart comparing within-subject and between-subject effects" style="max-width: 85%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 5.</em> Cliff's delta effect sizes for clinical variables comparing sessions included versus excluded from analysis (red = within-subject; blue = between-subject). Negative values indicate higher levels associated with exclusion; positive values indicate protective effects. * <em>p</em> < .05, ** <em>p</em> < .01, *** <em>p</em> < .001.</p>
</div>

---

## Key Findings

### Primary Result: Null Prediction of Ambiguity Tolerance

Ambiguity tolerance (γ) did not predict subsequent opioid use at either temporal lag (t+1: β = 0.25, *p* = .946; t+2: β = −0.45, *p* = .935). Adding γ to clinical covariate models did not improve fit, suggesting this parameter does not carry prospective clinical signal at the individual level in this sample.

### Missingness as a Clinically Informative Endpoint

Session exclusions were systematically associated with active substance use, elevated craving, sleep disturbance, and distress intolerance. Critically, predictors of UTOX positivity and predictors of exclusion showed **distinct clinical profiles** — pointing to different pathways to vulnerability and data quality failure.

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/oud_fig6_forest.png" alt="Forest plots of odds ratios for UTOX positivity and session exclusion" style="max-width: 85%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 6.</em> Forest plots of odds ratios (log₁₀ scale) for psychological factors associated with positive urine toxicology (blue, upper) and session exclusion (red, lower). Error bars represent 95% confidence intervals. * <em>p</em> ≤ .05, ** <em>p</em> ≤ .01. FDR-corrected.</p>
</div>

### Mediation: Clinical Vulnerability → UTOX → Dropout

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/oud_fig7_mediation.png" alt="Mediation analysis diagram showing paths through UTOX status" style="max-width: 85%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 7.</em> Mediation analysis: clinical factors → UTOX status (mediator) → session exclusion. Full mediation: anxiety, distress intolerance, craving, opioid withdrawal (effects fully explained by UTOX). Partial mediation: sleep disturbance (24% of effect through UTOX). No mediation: depression, positive affect, cognitive ability, negative affect (direct effects on session exclusion). Path coefficients shown with β and <em>p</em>-values.</p>
</div>

Craving, sleep disturbance, and distress intolerance operated primarily through active substance use, consistent with drug-seeking behaviour disrupting study engagement. Cognitive ability and positive affect exerted **direct protective effects** on session completion, independent of UTOX status.

Together, these findings argue that **missingness is a clinically informative endpoint** in dense-sampling designs, and that the distributional properties of retained data should not be assumed to represent the full clinical population.

---

## Propensity Score Correction

A secondary methodological contribution was the application of **inverse probability weighting (IPW)** to correct for the selection bias introduced by non-random session exclusion. Retained sessions were reweighted based on the predicted probability of exclusion from clinical covariates, adjusting the analysis sample to better approximate the full clinical distribution.

The null finding for γ persisted after IPW correction, strengthening the conclusion that ambiguity tolerance does not prospectively predict opioid use in this sample — rather than the null being an artefact of selective attrition.

---

## Discussion

The null prediction of γ on opioid use raises a deeper question: does ambiguity tolerance, as extracted from this paradigm, reflect a **stable individual trait with a neural substrate** — or is it more state-dependent, varying with clinical context? This question is directly addressed in a companion study using connectome-based predictive modelling in a healthy sample: [Whole-Brain Resting-State fMRI Prediction of Ambiguity Tolerance](/projects/4_project/).

---

## Code & Reproducibility

All analysis code is available at **[github.com/deng-hanwen/OUD_ambiguity_tolerance](https://github.com/deng-hanwen/OUD_ambiguity_tolerance)**, including R Markdown scripts for model fitting QC, logistic regression, propensity score weighting, mediation analysis, and visualisation. Raw data are not shared to protect participant confidentiality.

*MRes Dissertation, UCL / Yale University / Anna Freud Center. Supervised by Dr Sarah Yip & Dr Stephen Riley.*

---

## References

Konova, A. B., Lopez-Guzman, S., Urmanche, A., Ross, S., Louie, K., Rotrosen, J., & Glimcher, P. W. (2020). Computational markers of risky decision-making for identification of temporal windows of vulnerability to opioid use in people with opioid use disorder. *JAMA Psychiatry, 77*(4), 368–377.
