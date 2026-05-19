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

Bipolar disorder (BD) is characterised not only by episodic symptom states but by the *dynamics* of how mood moves over time — how quickly it shifts, how far it deviates, and how readily it returns to baseline. Understanding these dynamic properties offers a richer account of emotional vulnerability than static symptom ratings, and may yield computationally tractable biomarkers capable of prospectively indexing clinical risk.

This project investigates person-level affect dynamics in BD versus healthy controls (HC) using dense ecological momentary assessment (EMA) data from the **Mood Zoom** platform (5 assessments/day, up to 10 weeks; N = 94). The central question is: **do the dynamic properties of positive affect (PA) and negative affect (NA) differ between BD and HC, and do they prospectively predict changes in manic or depressive symptom severity?**

PA and NA composites were derived via principal component analysis (PCA) applied to six mood items (*Elated, Energetic, Irritable, Sad, Anxious, Angry*), and modelled using two complementary approaches operating at different analytical timescales.

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
| **η (eta)** | Oscillation frequency / lability | Coefficient of position (x). More negative η → higher oscillation frequency → greater emotional lability (more rapid, pronounced mood fluctuations). |
| **ζ (zeta)** | Dampening / resilience | Coefficient of velocity (ẋ). More negative ζ → stronger dampening → faster return to equilibrium → greater affective resilience. |

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

## Complementary Analysis: Linear Mixed-Effects (LME) Modelling

To complement the person-level DLO approach, an **LME model** was estimated at the observation level to examine *state-dependent* affect reactivity — specifically, whether the restoring force toward equilibrium varies with the current direction of mood movement, and whether this differs between BD and HC. Affect velocity was derived by fitting a natural cubic spline to each participant's time series and computing the instantaneous derivative, within-person standardised prior to modelling.

This dual-method design reflects a deliberate analytical distinction: DLO captures the **average dispositional properties** of the affect system over weeks, while LME captures **moment-to-moment state-dependent regulation** — two complementary windows onto the same underlying dynamics.

---

## Key Findings

Results indicate a **dissociation between PA and NA dynamics**, with the two affect streams showing qualitatively distinct relationships to clinical trajectories. Notably, NA dampening (ζ) emerged as a prospective predictor specifically associated with manic — not depressive — symptom change in BD, suggesting that the resilience of the negative affect system may carry information about vulnerability to mania that is not captured by positive affect dynamics or static symptom ratings alone.

At the observation level, BD participants showed greater state-dependent NA reactivity than HC, with the direction of current mood movement modulating the strength of the restoring force. Circadian organisation of affect velocity was also more pronounced in BD than HC, with group differences in morning affect dynamics identified for both PA and NA — consistent with disrupted diurnal emotion regulation in this population.

Together, DLO and LME analyses converge on a picture in which BD is characterised by systematically altered affect system dynamics, and in which individual differences in these dynamics carry prospective clinical signal.

---

## Code & Reproducibility

All analysis code is available at **[github.com/deng-hanwen/EMA-mood-dynamics](https://github.com/deng-hanwen/EMA-mood-dynamics)**, including R Markdown scripts for data QC, PCA, DLO model fitting and filtering, stepwise regression, LME modelling, and visualisation. Raw data are not shared to protect participant confidentiality.

*Manuscript in preparation. Co-authored with Dr Liam Mason (UCL).*

---

## References

Ollero, R., Estrada, E., Hunter, M. D., & Cáncer, P. F. (2025). Characterizing affect dynamics with a damped linear oscillator model: Theoretical considerations and recommendations for individual-level applications. *Psychological Methods, 30*(5), 1095–1112.
