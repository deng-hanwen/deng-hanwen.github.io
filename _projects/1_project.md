---
layout: page
title: Mood Velocity and Dynamics in Bipolar Disorder
description: Continuous-time dynamical systems modelling of ecological momentary assessment data to characterise affect lability and dampening in bipolar disorder
img: assets/img/proj_ema.png
importance: 1
category: research
github: https://github.com/deng-hanwen/EMA-mood-dynamics
related_publications: false
---

<p>
  <a href="https://github.com/deng-hanwen/EMA-mood-dynamics" class="btn btn-sm z-depth-0" role="button" style="background-color: #424242; color: white;">
    <i class="fab fa-github"></i> View Code on GitHub
  </a>
</p>

> **Note:** This project is currently being prepared for publication. Full methods and results will be made available upon submission.

---

## Overview

This project investigates the temporal dynamics of positive affect (PA) and negative affect (NA) in individuals with bipolar disorder (BD) compared to healthy controls (HC), using dense ecological momentary assessment (EMA) data collected via the Mood Zoom platform (5 assessments/day, up to 10 weeks; N = 94). The central aim is to extract person-level affect-dynamic parameters that prospectively index manic symptom intensification, providing computationally grounded biomarkers of mood instability beyond conventional symptom ratings.

PA and NA composites were derived via principal component analysis (PCA) applied to six mood items (*Elated, Energetic, Irritable, Sad, Anxious, Angry*), and modelled separately using two complementary approaches.

---

## Methods

### Damped Linear Oscillator (DLO) Modelling

Person-level affect dynamics were characterised using a **continuous-time state-space model** (DLO; OpenMx), implementing:

$$\ddot{x} = \eta \cdot \dot{x} + \zeta \cdot x$$

Two parameters were estimated per participant for each affect stream:

- **η (eta):** momentum — degree to which current velocity carries forward; less negative values reflect greater lability
- **ζ (zeta):** damping — strength of the restoring force toward equilibrium; more negative values reflect stronger pull-back

Solutions were accepted under a **stability criterion** requiring both system eigenvalues to have strictly negative real parts (Re(λ) < 0). Raw estimates were Winsorised at the 5th–95th percentile bounds (derived from stable participants) and transformed via inverse hyperbolic sine (asinh) to reduce skew while preserving sign.

Associations between DLO parameters and prospective manic and depressive symptom change (ΔAltman, ΔQIDS) were tested using **stepwise OLS regression** in the BD subsample, with Bonferroni correction applied across outcomes.

### Linear Mixed-Effects (LME) Modelling

To complement the person-level DLO analysis, an **LME model** was estimated at the observation level, examining state-dependent affect reactivity — specifically, whether BD and HC differ in how the restoring force varies with the current direction of mood movement. Mood velocity was derived by smoothing each participant's affect time series with a natural cubic spline and computing the instantaneous derivative, within-person standardised. Analyses also examined circadian patterning of affect velocity.

---

## Key Findings

Results indicate a dissociation between PA and NA dynamics, with the two affect systems showing distinct relationships to manic symptom trajectories. NA dampening (ζ) emerged as a mania-specific predictor, with a characteristic pattern of explained variance uniquely driven by manic — not depressive — symptom intensification. This effect was robust to outlier influence and replicated in sensitivity analyses.

At the observation level, BD participants showed greater state-dependent NA reactivity than HC, with the restoring force modulated by the current direction of mood movement. Circadian organisation of NA was also stronger in BD relative to HC, with group differences in morning affect velocity identified for both PA and NA.

DLO and LME approaches captured complementary aspects of affect dynamics: DLO reflects average dispositional properties of the mood system, while LME captures moment-to-moment state-dependent regulation.

---

## Code & Reproducibility

All analysis code is available at **[github.com/deng-hanwen/EMA-mood-dynamics](https://github.com/deng-hanwen/EMA-mood-dynamics)**, including R Markdown scripts for DLO model fitting, QC pipelines, stepwise regression, LME modelling, and visualisation. Raw data are not shared to protect participant confidentiality.

*Manuscript in preparation. Co-authored with Dr Liam Mason (UCL).*
