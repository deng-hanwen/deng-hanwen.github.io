---
layout: page
title: Computational Markers and Clinical Vulnerability in Early OUD Treatment
description: MRes dissertation — utility-based computational modelling of a risk and ambiguity decision-making task in methadone treatment, with propensity score correction for non-random missingness
img: assets/img/oud_thumb.png
importance: 2
category: Computational and Neuroimaging
related_publications: false
---

*UCL / Yale University / Anna Freud Center. Supervised by Dr Sarah Yip & Dr Stephen Riley. Collaborators: Anna Konova & Francesca M. LoFaro.*

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

Participants completed a 120-trial incentive-compatible decision-making task (Konova et al., 2020) across two interleaved contexts. On each trial, participants chose between a guaranteed **$5** and a lottery offering a reward value *v* ($5–$66) or $0:

- **Known-risk context (120 trials):** The lottery probability *p* was explicitly stated (25%, 50%, or 75%), represented by a physical bag of 100 coloured chips with the exact composition specified. Participants could inspect the bags after the experiment. Each combination of *p* and *v* appeared once, yielding a full factorial design across probability and value levels.

- **Ambiguity context (120 trials):** The probability information was partially occluded by a grey bar covering either 24%, 50%, or 74% of the display (*A* = low, medium, or high ambiguity). The true underlying probability was fixed at 50% on all ambiguity trials — only the amount of *visible* information varied. Participants therefore faced genuine uncertainty about the outcome probability rather than a subjective estimate of a known distribution.

The task was incentive-compatible: at session end, one trial was randomly selected and played out to determine a variable bonus (either the guaranteed $5 or the lottery outcome), ensuring participants were motivated to express their true preferences.

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

## Key Findings

#### Clinical Predictors of Data Quality

Session exclusion was not random: UTOX-positive sessions were **6.8× more likely** to be excluded, revealing that data quality itself indexes active substance use. This motivated two additional analyses: logistic regression identifying predictors of exclusion, and propensity score weighting to correct for the selection bias introduced by non-random dropout.

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/oud_fig5_cliffs.png" alt="Cliff's delta bar chart comparing within-subject and between-subject effects" style="max-width: 85%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 3.</em> Cliff's delta effect sizes for clinical variables comparing included versus excluded sessions (red = within-subject; blue = between-subject). Negative values indicate higher levels of a variable associated with session exclusion; positive values indicate protective effects. * <em>p</em> < .05, ** <em>p</em> < .01, *** <em>p</em> < .001.</p>
</div>

#### Missingness as a Clinically Informative Endpoint

Ambiguity tolerance (γ) did not predict subsequent opioid use at either temporal lag (t+1: β = 0.25, *p* = .946; t+2: β = −0.45, *p* = .935). While the primary hypothesis was not supported, predictors of UTOX positivity and predictors of session exclusion showed **distinct clinical profiles**, pointing to different pathways to clinical vulnerability and data quality failure.

#### Mediation: Clinical Vulnerability → UTOX → Dropout

Craving, sleep disturbance, and distress intolerance operated primarily through active substance use, consistent with drug-seeking behaviour disrupting study engagement. Cognitive ability and positive affect exerted **direct protective effects** on session completion, independent of UTOX status. Together, these findings argue that **missingness is a clinically informative endpoint** in dense-sampling designs, and that the distributional properties of retained data should not be assumed to represent the full clinical population.

---

## Discussion

The null prediction of γ is, at face value, a null — but it may also point toward something worth examining. γ may be **state-dependent**: estimated from noisy behavioural data in individuals whose cognitive capacity fluctuates with withdrawal, craving, and sleep, it may capture transient state rather than stable trait. Under this interpretation, the null does not mean ambiguity tolerance is clinically irrelevant — it means the right measurement context has not yet been found.

This reading is supported by a growing reliability literature. Harlé et al. (2019) found that *variability* in decision-making parameters — not mean levels — predicted methamphetamine relapse. Karvelis et al. (2024) report ICCs below 0.5 for most computational measures, with state-like fluctuations dominating within-subject variance; Karvelis & Diaconescu (2025) show this creates a **reliability paradox** where genuine biomarkers appear uninformative because noise suppresses detectable group differences. Zorowitz & Niv (2023) identify poor test-retest reliability as a core driver of inconsistent replication. For a comprehensive treatment, see [Karvelis et al. (2023)](https://www.sciencedirect.com/science/article/pii/S0149763423001069).

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/oud_reliability_stability.png" alt="Decomposition of test-retest reliability into measurement error and performance change components across time" style="max-width: 90%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 4.</em> Reliability and stability of computational measures. Test-retest reliability (y-axis) decomposes into fixed measurement error (task design, model fitting) and performance change components (practice effects, trait-like changes, and state-like changes). The large state-like fluctuation component (yellow) reflects transient within-person variation that reduces observed reliability — and attenuates apparent effect sizes — even when the underlying trait is stable. Reproduced from Karvelis et al. (2023).</p>
</div>

This opens a direct question: **does ambiguity tolerance show stable individual-difference structure when estimated from a neural rather than behavioural substrate?** The companion study addresses this using CPM in resting-state fMRI: [Whole-Brain Resting-State fMRI Prediction of Ambiguity Tolerance](/projects/4_project/).

The missingness findings offer a methodological contribution: UTOX-positive sessions — the clinically most relevant — are also the most likely to be excluded, creating a systematic blind spot. **Missingness patterns carry clinical signal that complementary analyses can recover**, and dense-sampling designs should pre-register dropout as a co-primary outcome.

An emerging direction moves beyond single-parameter biomarker logic toward **computational fingerprints** — treating the joint profile of α, γ, and μ across sessions as a multi-dimensional signature of each person's decision-making phenotype. [This framing](https://www.sciencedirect.com/science/article/pii/S2451902226000534) is illustrated below: computational snapshots evolve differently across biotypes and recovery trajectories, offering a richer, person-centred view of clinical change than any single parameter can provide.

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/oud_fingerprint_panel.png" alt="Computational snapshots over time: radar charts showing multi-parameter profiles across biotypes and timepoints" style="max-width: 95%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 5.</em> Computational snapshots over time across biotypes and recovery trajectories (Persons 1–4) and a healthy control. Each radar chart plots the joint multi-parameter computational profile at one session; the profile shape and size evolve distinctly depending on biotype and clinical trajectory. Reproduced from <a href="https://www.sciencedirect.com/science/article/pii/S2451902226000534"><em>Biological Psychiatry: CNNI</em> (2026)</a>.</p>
</div>

---

## Code & Reproducibility

Analysis code for this project was developed collaboratively and the project is ongoing. Code is not publicly available at this stage. Raw data are not shared to protect participant confidentiality.

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
