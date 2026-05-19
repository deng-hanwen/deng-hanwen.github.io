---
layout: page
title: Mood Velocity and Dynamics in Bipolar Disorder
description: Continuous-time dynamical systems modelling of EMA mood data to characterise affect lability and dampening in bipolar disorder
img: assets/img/proj_ema.png
importance: 1
category: research
github: https://github.com/deng-hanwen/EMA-mood-dynamics
related_publications: false
---

<div class="row">
  <div class="col-sm-12">
    <p>
      This project investigates the temporal dynamics of positive and negative affect in individuals 
      with bipolar disorder (BD) relative to healthy controls (HC), using continuous-time 
      dynamical systems modelling applied to dense ecological momentary assessment (EMA) data.
      A key aim is to identify affect-dynamic parameters that prospectively index manic symptom 
      intensification — providing computationally grounded, individual-level biomarkers of mood 
      instability beyond conventional symptom ratings.
    </p>
    <p>
      <a href="https://github.com/deng-hanwen/EMA-mood-dynamics" class="btn btn-sm z-depth-0" role="button" style="background-color: #424242; color: white;">
        <i class="fab fa-github"></i> View Code on GitHub
      </a>
    </p>
  </div>
</div>

---

## Study Design

**Participants.** A total of 94 participants (BD and HC) were recruited as part of a larger longitudinal study. Following quality control and DLO stability screening, 81 participants yielded valid DLO parameter estimates. Mania severity was assessed at baseline and study end using the Altman Self-Rating Mania Scale (ASRM; Altman et al., 1997) and depressive severity using the Quick Inventory of Depressive Symptomatology (QIDS; Rush et al., 2003). Symptom intensification was indexed as the change from baseline to endpoint (dAltman = Last − First ASRM; dQIDS = Last − First QIDS).

**EMA Procedure.** Participants completed five mood assessments per day over up to 10 weeks via the Mood Zoom platform. Each survey included ratings of six items — *Elated, Energetic, Irritable, Sad, Anxious*, and *Angry* — on a 1–7 Likert scale.

**Affect Score Derivation.** Principal component analysis (PCA) was applied to the six mood items pooled across all participants and time points. Items were *z*-scored within the combined sample prior to PCA to place all ratings on a common scale. Two components were retained: PC1 captured a general negative affect / valence dimension (highest loadings: Sad, Anxious, Angry, Irritable) and PC2 captured an activated positive affect dimension (highest loadings: Elated, Energetic). **Negative Affect (NA)** was operationalised as PC1 scores and **Positive Affect (PA)** as PC2 scores. DLO parameters were estimated separately for PA and NA.

---

## Methods

### Damped Linear Oscillator (DLO) Modelling

DLO parameters were estimated per participant using a **continuous-time state-space model** fitted via maximum likelihood (OpenMx; Boker et al., 2011), implementing the damped linear oscillator equation:

$$\ddot{x} = \eta \cdot \dot{x} + \zeta \cdot x$$

where *x* denotes displacement from equilibrium, $$\dot{x}$$ velocity, and $$\ddot{x}$$ acceleration. Two parameters of theoretical interest were extracted:

- **η (eta):** captures momentum — the degree to which current velocity carries forward; less negative values indicate greater affect lability.
- **ζ (zeta):** captures damping — the strength of the restoring force pulling the system back toward equilibrium; more negative values indicate a stronger pull-back.

The state-space formulation accommodates irregularly spaced observations and inter-segment gaps via the matrix exponential of the system matrix. A **stability criterion** was applied: solutions were classified as stable if both eigenvalues of the system matrix had strictly negative real parts (Re(λ) < −tol), indicating that the mood system returns to equilibrium. The majority of participants were overdamped (ζ < 0), indicating monotonic return to equilibrium without oscillation.

**Pre-analysis transformations.** Raw η and ζ estimates were Winsorised at the 5th–95th percentile bounds derived from stable participants only (to prevent divergent estimates from distorting clip thresholds), followed by an inverse hyperbolic sine (asinh) transformation to reduce skew while preserving sign.

### Stepwise OLS Regression

Stepwise ordinary least squares (OLS) regressions tested whether manic and depressive symptom intensification predicted person-level DLO parameters within the BD-stable subsample. Five hierarchical models were estimated per outcome:

| Model | Predictors |
|-------|-----------|
| M1 | Baseline mania severity (*z*-ASRM) |
| M2 | M1 + manic symptom intensification (dAltman) |
| M3 | Baseline depression (*z*-QIDS) + baseline mania (*z*-ASRM) |
| M4 | M3 + depressive symptom intensification (dQIDS) |
| M5 | Full model: all four predictors |

Bonferroni correction was applied for testing two outcomes (η and ζ) per affect stream (threshold *p* < .025). Huber M-estimation was used to assess outlier influence via partial regression plots; OLS estimates were used for all inferential tests.

### Linear Mixed-Effects (LME) Modelling

To complement the person-level DLO analysis, a **linear mixed-effects model** was estimated at the observation level. Mood velocity (*v*) was derived per participant by smoothing the affect time series with a natural cubic spline, computing the instantaneous derivative at each observation, and within-person standardising. The model tested whether BD and HC differed in the state-dependent structure of affect dynamics — specifically, how the restoring force varies with the direction of current mood movement.

---

## Key Findings

### NA Dampening Prospectively Indexes Manic Symptom Intensification

The primary finding concerns **NA ζ ~ dAltman**: greater manic symptom intensification was associated with more negative NA ζ (stronger pull-back toward equilibrium). The R² trajectory across the stepwise hierarchy showed a characteristic spike-and-collapse pattern:

| Model | R² |
|-------|----|
| M1 (baseline mania only) | .000 |
| M2 (+dAltman) | .091 |
| M3 (depression replaces dAltman) | .000 |
| M5 (full model) | .100 |

This pattern — R² collapsing when dAltman is removed and recovering when it is reintroduced — identifies dAltman as the unique driver of variance in NA ζ, with no contribution from depression. The effect was robust to log-transformation (b = −0.469, *p* = .027), confirming that the association is not an artefact of outliers. A sensitivity analysis restricting to the first month of EMA data replicated the R² pattern, though clinical predictors were attenuated, consistent with reduced power in the shorter window.

### PA Lability and Mania: Outlier-Driven Effect

A trend was observed for **PA η ~ dAltman** (greater mania → greater PA lability), but this effect did not survive log-transformation, indicating it was driven by a single influential observation. PA and NA therefore appear to reflect dissociable dynamical processes with distinct relationships to manic symptom trajectories.

### LME: State-Dependent Affect Reactivity in BD

The LME analysis revealed that **BD participants exhibited greater state-dependent NA reactivity** than HC: the velocity × displacement interaction (v_lag_z × x_lag_z: GroupHC = +0.045, *p* < .05) indicates that, in BD, the restoring force is modulated by the current direction of NA movement — braking harder when NA is elevated and still rising. In HC, the restoring force is approximately uniform with respect to displacement direction.

A **circadian rhythm effect** was also identified: within BD, NA showed significant circadian organisation (sin₂₄ = −0.094, *p* < .001), whereas PA did not. HC exhibited significantly faster morning affect velocity than BD for both PA (b = +0.034, *p*_FDR = .009) and NA (b = +0.040, *p*_FDR = .002).

---

## Interpretation

The dissociation between PA and NA dynamics parallels theoretical accounts in which mania involves dysregulated approach motivation (reflected in PA lability) alongside a paradoxically strengthened NA dampening system. The NA ζ ~ dAltman association — mania-specific, robust, and replicated across subsamples — suggests that heightened NA dampening may operate as a vulnerability marker: by rapidly suppressing negative affect, the system may lower the threshold for upward mood excursions. These findings are consistent with dynamical systems accounts of mood instability in BD and contribute to ongoing efforts to derive computationally grounded, individual-level biomarkers with translational relevance.

---

## Code & Reproducibility

All analysis code is available at **[github.com/deng-hanwen/EMA-mood-dynamics](https://github.com/deng-hanwen/EMA-mood-dynamics)**. The repository includes R Markdown scripts for DLO model fitting, QC pipelines, stepwise regression, LME modelling, and visualisation. Raw data are not shared to protect participant confidentiality.

*Manuscript in preparation. Co-authored with Dr Liam Mason (UCL).*
