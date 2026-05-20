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

*UCL / Yale University / Anna Freud Center. Supervised by Dr Sarah Yip & Dr Stephen Riley.*

> **Note:** MRes Dissertation — Distinction.

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

Choices were modelled using an **expected utility framework** adapted from Konova et al. (2020), with three free parameters. The utility of the lottery option is:

$$\text{EU}(\text{lottery}) = \left[p - \beta \cdot \frac{A}{2}\right] v^{\alpha}$$

where *p* is the known probability, *A* is ambiguity level, *v* is reward value, α captures the curvature of utility over outcomes (risk tolerance), and β = 1 − γ scales the ambiguity adjustment (higher β = greater ambiguity aversion; higher γ = greater ambiguity tolerance). Choices were linked to utilities via a softmax decision rule:

$$P(\text{choose lottery}) = \frac{1}{1 + e^{-\mu \cdot \Delta\text{EU}}}$$

where ΔEU = EU(lottery) − EU(safe option) and μ is the inverse temperature (choice sensitivity).

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

The null prediction of γ is, at face value, a null — but it may also point toward something worth examining. Two interpretations are worth considering. First, ambiguity tolerance as measured by this paradigm may not reflect the particular decision-making vulnerability that drives relapse in early MOUD — the task was designed for a healthy population, and its sensitivity to individual differences in a clinically burdened, state-fluctuating sample may be attenuated. Second, and more fundamentally, γ may be **state-dependent**: estimated session-by-session from noisy behavioural data in individuals whose cognitive capacity and motivation fluctuate with withdrawal, craving, and sleep, it may capture transient state rather than stable trait. Under this interpretation, the null does not mean ambiguity tolerance is clinically irrelevant — it means the right measurement context has not yet been found.

This interpretation is consistent with a growing body of evidence that clinical and environmental state substantially contaminates behavioural computational parameters. Reiter et al. (2019) demonstrated that social and contextual factors — in this case peer influence during risky choice — directly modulate reinforcement learning parameters in ways that are typically attributed to stable individual differences. In treatment populations specifically, Harlé et al. (2019) found that it was *variability* in decision-making parameters across sessions, not mean levels, that predicted methamphetamine relapse, suggesting that within-person fluctuation carries signal that cross-sectional approaches miss. The broader reliability literature is sobering: Karvelis et al. (2024) reported intraclass correlation coefficients below 0.5 for the majority of behavioural and computational measures across repeat sessions, with state-like within-subject fluctuations accounting for a substantial proportion of total variance. This psychometric challenge is compounded by what Karvelis & Diaconescu (2025) term the **reliability paradox**: poor measurement reliability systematically attenuates effect sizes and group differences, making genuine biomarkers appear clinically uninformative even when the underlying construct is valid. Zorowitz & Niv (2023) have argued that this problem — low test-retest reliability producing inconsistent cross-study replication — is among the most pressing unresolved issues in computational psychiatry. For a comprehensive roadmap of the psychometric and clinical translation challenges facing the field, see [Karvelis et al. (2023)](https://www.sciencedirect.com/science/article/pii/S0149763423001069).

This opens a direct question: **does ambiguity tolerance, when estimated from a neural rather than behavioural substrate, show the stable individual-difference structure that would make it a viable biomarker?** This is precisely what the companion study addresses using connectome-based predictive modelling (CPM) in a resting-state fMRI dataset: [Whole-Brain Resting-State fMRI Prediction of Ambiguity Tolerance](/projects/4_project/).

The missingness finding adds a second, methodological contribution. Dense-sampling designs in treatment contexts carry an underappreciated assumption: that participants who complete sessions are representative of the broader clinical population. The present results show they are not. UTOX-positive sessions — the sessions most likely to capture the clinically relevant states of active relapse — are precisely the sessions most likely to be lost to exclusion. There is a broader structural tension here: the populations of greatest clinical interest may be exactly those least suited to complete research protocols, introducing a systematic gap between studied and target populations. The laboratory-to-clinic translation problem compounds this: Buelow et al. (2024) showed that intact laboratory task performance can coexist with significant real-world functional impairment, raising questions about whether paradigms developed in controlled settings capture ecologically valid behaviour. Together, these findings argue that our models are fitted on data from participants who are, on balance, doing relatively well. **Missingness patterns carry clinical signal that complementary analyses can recover**, and future trials using dense behavioural paradigms should pre-register dropout as a co-primary outcome alongside the computational parameters themselves.

A complementary direction for future work concerns the unit of analysis itself. The present study — like most in the field — extracts a small number of scalar parameters and tests each as a standalone predictor. An emerging alternative is to treat the full multi-parameter profile as a **computational fingerprint**: rather than asking whether γ alone predicts outcome, one asks whether the joint configuration of α, γ, and μ — combined with session-level clinical variables — uniquely characterises each individual's decision-making profile in a way that tracks clinical change. [This framing](https://www.sciencedirect.com/science/article/pii/S2451902226000534) moves computational psychiatry away from single-biomarker logic and toward a richer, person-centred representation of cognitive vulnerability.

---

## Code & Reproducibility

All analysis code is available at **[github.com/deng-hanwen/OUD_ambiguity_tolerance](https://github.com/deng-hanwen/OUD_ambiguity_tolerance)**, including R Markdown scripts for model fitting QC, logistic regression, propensity score weighting, mediation analysis, and visualisation. Raw data are not shared to protect participant confidentiality.

---

## References

Buelow, M. T., Barnhart, W. R., & Schult, J. C. (2024). Does lab performance predict real-world decision-making outcomes? A meta-analysis of performance-based decision-making measures. *Journal of Clinical and Experimental Neuropsychology, 46*(3), 187–206.

Harlé, K. M., Yu, A. J., & Paulus, M. P. (2019). Bayesian computational markers of relapse in methamphetamine dependence. *NeuroImage: Clinical, 22*, 101794.

Karvelis, P., Paulus, M. P., & Diaconescu, A. O. (2023). [Individual differences in computational psychiatry: A review of current challenges.](https://www.sciencedirect.com/science/article/pii/S0149763423001069) *Neuroscience & Biobehavioral Reviews, 148*, 105137.

Karvelis, P., Charlton, C. E., Romaniuk, L., Hall, J., Whalley, H. C., & Diaconescu, A. O. (2024). Test-retest reliability of behavioral and computational measures of advice taking under volatility. *PLOS ONE, 19*(5), e0302803.

Karvelis, P., & Diaconescu, A. O. (2025). Clarifying the reliability paradox: Poor measurement reliability attenuates group differences. *Frontiers in Psychology, 15*, 1305773.

Konova, A. B., Lopez-Guzman, S., Urmanche, A., Ross, S., Louie, K., Rotrosen, J., & Glimcher, P. W. (2020). Computational markers of risky decision-making for identification of temporal windows of vulnerability to opioid use in people with opioid use disorder. *JAMA Psychiatry, 77*(4), 368–377.

Reiter, A. M. F., Suzuki, S., O'Doherty, J. P., Li, S.-C., & Eppinger, B. (2019). Risk contagion by peers affects learning and decision-making in adolescents. *Journal of Experimental Psychology: General, 148*(9), 1494–1504.

Zorowitz, S., & Niv, Y. (2023). Improving the reliability of cognitive task measures: A narrative review. *Biological Psychiatry: Cognitive Neuroscience and Neuroimaging, 8*(8), 789–797.
