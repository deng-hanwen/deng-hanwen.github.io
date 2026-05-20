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

## Expected Utility Model

Choices were modelled using an **expected utility framework** adapted from Konova et al. (2020), with three free parameters:

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/oud_model.png" alt="Expected utility model: utility equation and probabilistic choice rule" style="max-width: 90%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 3.</em> Expected utility model. Top: utility equation for the lottery option, where <em>p</em> is the known risk probability, <em>β</em> scales the ambiguity adjustment (higher β = greater ambiguity aversion), <em>A</em> is ambiguity level, and α is the risk tolerance (curvature of the utility function). Bottom: softmax decision rule. Reproduced from Konova et al. (2020).</p>
</div>

| Parameter | Name | Interpretation |
|-----------|------|----------------|
| **α (alpha)** | Risk tolerance | Curvature of utility over outcomes; α < 1 = risk aversion |
| **γ (gamma)** | Ambiguity tolerance | Subjective adjustment of ambiguous probabilities; higher = more willing to engage with uncertainty |
| **μ (mu)** | Choice sensitivity | Inverse temperature of the softmax; lower = noisier choices |

Parameters were estimated per session via maximum likelihood estimation. Inclusion required *R*² ≥ 0.10 and parameter bounds checks on α and μ.

---

## Clinical Predictors of Data Quality

Session exclusion was not random: UTOX-positive sessions were **6.8× more likely** to be excluded, revealing that data quality itself indexes active substance use. This motivated two additional analyses: logistic regression identifying predictors of exclusion, and propensity score weighting to correct for the selection bias introduced by non-random dropout.

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/oud_fig5_cliffs.png" alt="Cliff's delta bar chart comparing within-subject and between-subject effects" style="max-width: 85%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 4.</em> Cliff's delta effect sizes for clinical variables comparing included versus excluded sessions (red = within-subject; blue = between-subject). Negative values indicate higher levels of a variable associated with session exclusion; positive values indicate protective effects. * <em>p</em> < .05, ** <em>p</em> < .01, *** <em>p</em> < .001.</p>
</div>

---

## Key Findings

### Missingness as a Clinically Informative Endpoint

Ambiguity tolerance (γ) did not predict subsequent opioid use at either temporal lag (t+1: β = 0.25, *p* = .946; t+2: β = −0.45, *p* = .935). While the primary hypothesis was not supported, predictors of UTOX positivity and predictors of session exclusion showed **distinct clinical profiles**, pointing to different pathways to clinical vulnerability and data quality failure.

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/oud_fig6_forest.png" alt="Forest plots of odds ratios for UTOX positivity and session exclusion" style="max-width: 85%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 5.</em> Forest plots of odds ratios (log₁₀ scale) for psychological factors associated with positive urine toxicology (blue, upper) and session exclusion (red, lower). Error bars represent 95% confidence intervals. * <em>p</em> ≤ .05, ** <em>p</em> ≤ .01. FDR-corrected.</p>
</div>

### Mediation: Clinical Vulnerability → UTOX → Dropout

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/oud_fig7_mediation.png" alt="Mediation analysis diagram showing paths through UTOX status" style="max-width: 85%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 6.</em> Mediation analysis: clinical factors → UTOX status (mediator) → session exclusion. Full mediation: anxiety, distress intolerance, craving, opioid withdrawal. Partial mediation: sleep disturbance (24% reduction via UTOX). No mediation: depression, positive affect, cognitive ability, negative affect (direct effects). Path coefficients shown with β and <em>p</em>-values.</p>
</div>

Craving, sleep disturbance, and distress intolerance operated primarily through active substance use, consistent with drug-seeking behaviour disrupting study engagement. Cognitive ability and positive affect exerted **direct protective effects** on session completion, independent of UTOX status. Together, these findings argue that **missingness is a clinically informative endpoint** in dense-sampling designs, and that the distributional properties of retained data should not be assumed to represent the full clinical population.

---

## Propensity Score Correction

A secondary methodological contribution was the application of **inverse probability weighting (IPW)** to correct for the selection bias introduced by non-random session exclusion. Retained sessions were reweighted based on the predicted probability of exclusion from clinical covariates, adjusting the analysis sample to better approximate the full clinical distribution. The null finding for γ persisted after IPW correction, ruling out selective attrition as an explanation.

---

## Discussion

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/oud_discussion_framework.png" alt="Conceptual framework interpreting the null finding and missingness" style="max-width: 98%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 7.</em> Conceptual framework summarising the two-pronged interpretation of study findings. Left branch: the null prediction of γ, confirmed robust to attrition bias by IPW correction, raises a fundamental question about parameter interpretability. Right branch: non-random session exclusion as a clinical endpoint in its own right, mediated through active substance use.</p>
</div>

The null prediction of γ is not merely a negative result — it is a theoretically informative one. Two interpretations are possible. First, ambiguity tolerance as measured by this paradigm may not reflect the particular decision-making vulnerability that drives relapse in early MOUD — the task was designed for a healthy population, and its sensitivity to individual differences in a clinically burdened, state-fluctuating sample may be attenuated. Second, and more fundamentally, γ may be **state-dependent**: estimated session-by-session from noisy behavioural data in individuals whose cognitive capacity and motivation fluctuate with withdrawal, craving, and sleep, it may capture transient state rather than stable trait. Under this interpretation, the null does not mean ambiguity tolerance is clinically irrelevant — it means the right measurement context has not yet been found.

The IPW-corrected null strengthens this interpretation: it rules out attrition bias as a confound, making state-dependent noise the more parsimonious explanation. This opens a direct question: **does ambiguity tolerance, when estimated from a neural rather than behavioural substrate, show the stable individual-difference structure that would make it a viable biomarker?** This is precisely what the companion study addresses using connectome-based predictive modelling (CPM) in a resting-state fMRI dataset: [Whole-Brain Resting-State fMRI Prediction of Ambiguity Tolerance](/projects/4_project/).

The missingness finding adds a second, methodological contribution. Dense-sampling designs in treatment contexts carry an underappreciated assumption: that participants who complete sessions are representative of the broader clinical population. The present results show they are not. UTOX-positive sessions — the sessions most likely to capture the clinically relevant states of active relapse — are precisely the sessions most likely to be lost to exclusion. This creates a systematic blind spot: our models are fitted on data from participants who are, on balance, doing relatively well. **Missingness patterns carry clinical signal that complementary analyses can recover**, and future trials using dense behavioural paradigms should pre-register dropout as a co-primary outcome alongside the computational parameters themselves.

---

## Code & Reproducibility

All analysis code is available at **[github.com/deng-hanwen/OUD_ambiguity_tolerance](https://github.com/deng-hanwen/OUD_ambiguity_tolerance)**, including R Markdown scripts for model fitting QC, logistic regression, propensity score weighting, mediation analysis, and visualisation. Raw data are not shared to protect participant confidentiality.

*MRes Dissertation, UCL / Yale University / Anna Freud Center. Supervised by Dr Sarah Yip & Dr Stephen Riley.*

---

## References

Konova, A. B., Lopez-Guzman, S., Urmanche, A., Ross, S., Louie, K., Rotrosen, J., & Glimcher, P. W. (2020). Computational markers of risky decision-making for identification of temporal windows of vulnerability to opioid use in people with opioid use disorder. *JAMA Psychiatry, 77*(4), 368–377.
