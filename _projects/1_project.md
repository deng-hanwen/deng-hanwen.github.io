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

Existing EMA studies of bipolar disorder (BD) estimate average mood dynamics across the study period, missing how affect evolves *within a person* as an episode approaches. The **Damped Linear Oscillator (DLO)** model offers an alternative: mechanistically suited to BD's oscillatory timescale, it captures two dynamic signatures — **momentum** (η) and **damping** (ζ) — in continuous time.

This project applies DLO modelling to dense EMA data (N = 94 BD + HC, 5 assessments/day, up to 8 weeks), testing whether DLO parameters are sensitive to prospective manic and depressive symptom change. PA and NA composites were derived via PCA from six mood items (*Elated, Energetic, Irritable, Sad, Anxious, Angry*).

---

## The Damped Linear Oscillator (DLO) Model

The primary modelling approach treats each person's affect time series as the output of a **damped linear oscillator** — a continuous-time dynamical system that describes oscillatory processes governed by both a restoring force and a dampening force.

The model is specified as a state-space system in continuous time (SSM-CT), with dynamics governed by the following equation (Ollero et al., 2025):

$$\begin{bmatrix} \dot{x} \\ \ddot{x} \end{bmatrix} = \begin{bmatrix} 0 & 1 \\ \eta & \zeta \end{bmatrix} \begin{bmatrix} x \\ \dot{x} \end{bmatrix} + \begin{bmatrix} 0 \\ q(t) \end{bmatrix}$$

where $$x$$ is the momentary affect state, $$\dot{x}$$ is the rate of change in affect (velocity), $$\ddot{x}$$ is the acceleration, and $$q(t)$$ captures random environmental perturbations (dynamic noise). In scalar form, the dynamic equation is:

$$\ddot{x} = \eta x + \zeta \dot{x}$$

Two parameters fully characterise the system's dynamics:

| Parameter | Name | Interpretation |
|-----------|------|----------------|
| **η (eta)** | Momentum / lability | Coefficient of position (x). More negative η → higher oscillation frequency → greater affective lability. |
| **ζ (zeta)** | Damping / resilience | Coefficient of velocity (ẋ). More negative ζ → stronger damping → faster return to equilibrium → greater resilience. |

<br>

A useful intuition comes from the **ball-in-bowl metaphor** (Ollero et al., 2025): imagine mood as a ball rolling inside a bowl. The curvature of the bowl corresponds to η — a steeper bowl (more negative η) produces stronger oscillations and a higher oscillation frequency. The surface texture represents ζ — a velvet-lined bowl (more negative ζ) creates greater friction, slowing the ball and returning it to the centre more quickly.

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/dlo_fig1_bowl.png" alt="Ball-in-bowl metaphor for DLO model" style="max-width: 80%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 1.</em> Ball-in-bowl metaphor illustrating DLO dynamics: (A) ball at equilibrium; (B) ball displaced from equilibrium. Reproduced from Ollero et al. (2025, <em>Psychological Methods</em>).</p>
</div>

The effects of varying η and ζ on affect trajectories are illustrated in Figures 2 and 3 below. Individuals with greater lability (η closer to zero) oscillate more slowly, while stronger dampening (more negative ζ) produces faster convergence back to the equilibrium.

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/dlo_fig23_trajectories.png" alt="Affect trajectories for different values of eta and zeta" style="max-width: 95%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figures 2–3.</em> Simulated affect trajectories illustrating the effect of varying η (emotional lability, left) and ζ (resilience, right). Reproduced from Ollero et al. (2025, <em>Psychological Methods</em>).</p>
</div>

The DLO was fitted as a **continuous-time state-space model** using **OpenMx** in R. This specification accommodates the irregular inter-observation intervals inherent in naturalistic EMA data and yields parameters directly comparable across datasets with different sampling rates. Individual solutions were accepted under a **stability criterion** requiring both system eigenvalues to have strictly negative real parts (Re(λ) < 0). Raw estimates were Winsorised at the 5th–95th percentile bounds (derived from stable participants) and transformed via inverse hyperbolic sine (asinh) to reduce skew while preserving sign.

Associations between DLO parameters and prospective manic and depressive symptom change (ΔAltman, ΔQIDS) were tested using **stepwise OLS regression** in the BD subsample, with Bonferroni correction applied across outcomes.

---

## Control Analysis: Linear Mixed-Effects (LME) Modelling

An **LME model** fitted to moment-to-moment mood scores served as a control analysis, testing whether the associations between symptom change and affect dynamics were detectable without the DLO framework. Within the LME, restoring force is approximated by the coefficient on current affect state (x), and momentum by the coefficient on its lagged value (x_{t-1}):

$$x_{ti} \sim \underbrace{\beta_1 x_{ti}}_{\text{restoring force}} + \underbrace{\beta_2 x_{(t-1)i}}_{\text{momentum}} + \cdots$$

The comparison is deliberate: DLO estimates these as continuous-time system parameters from the full trajectory, while LME treats them as discrete-lag regression coefficients — a coarser approximation that does not capture the oscillatory structure.

---

## Key Findings

Greater manic worsening was associated with increased PA lability (η) and altered NA damping (ζ), with both signatures specifically linked to mania rather than depression — spanning both affect streams. Critically, neither finding was detectable using LME, underscoring the necessity of DLO for capturing relapse-relevant mood dynamics.

---

## Code & Reproducibility

All analysis code is available at **[github.com/deng-hanwen/EMA-mood-dynamics](https://github.com/deng-hanwen/EMA-mood-dynamics)**, including R Markdown scripts for data QC, PCA, DLO model fitting and filtering, stepwise regression, LME modelling, and visualisation. Raw data are not shared to protect participant confidentiality.

*Manuscript in preparation. Co-authored with Dr Liam Mason (UCL).*

---

## References

Ollero, R., Estrada, E., Hunter, M. D., & Cáncer, P. F. (2025). Characterizing affect dynamics with a damped linear oscillator model: Theoretical considerations and recommendations for individual-level applications. *Psychological Methods, 30*(5), 1095–1112.
