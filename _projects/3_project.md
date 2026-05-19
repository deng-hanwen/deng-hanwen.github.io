---
layout: page
title: Computational Markers and Clinical Vulnerability in Early OUD Treatment
description: MRes dissertation — utility-based computational modelling of a risk and ambiguity decision-making task in methadone treatment, with propensity score correction for non-random missingness
img: assets/img/5.jpg
importance: 2
category: research
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

The study uses a dense longitudinal design: 15 participants completed a Risk and Ambiguity Decision-Making Task across up to 8 weekly sessions, alongside urine toxicology screening (UTOX) and comprehensive clinical assessments (craving, withdrawal, affect, sleep, cognitive ability).

A secondary question emerged from the data itself: **34.5% of planned sessions were excluded** for poor behavioural quality. Rather than treating this as nuisance, the project investigates whether exclusion patterns carry clinical signal — and corrects for the resulting bias.

---

## Methods

### Computational Model

Choices were modelled using an **expected utility framework** with three free parameters:

- **α (alpha):** risk tolerance — curvature of the utility function over outcomes
- **γ (gamma):** ambiguity tolerance — subjective adjustment applied to ambiguous probabilities
- **β (beta):** choice sensitivity (inverse temperature of the softmax decision rule)

Parameters were estimated per session using maximum likelihood. Model fit was assessed via *R*² ≥ 0.10 and bounds checks on α and β.

### Primary Analysis

Ambiguity tolerance (γ) was tested as a time-lagged predictor of prospective opioid use (UTOX positivity at *t*+1 and *t*+2) using mixed-effects logistic regression, controlling for clinical covariates.

### Handling Missingness as Clinical Signal

Session exclusions were **not random**: positive UTOX was strongly associated with session exclusion, revealing that data quality itself indexes active substance use. This motivated two additional analyses:

1. **Exclusion as outcome** — logistic regression identifying predictors of session exclusion
2. **Propensity score weighting** — inverse probability weighting applied to retained sessions to correct for the selection bias introduced by non-random exclusion

### Mediation Analysis

A mediation framework tested whether the relationship between baseline clinical vulnerability and data dropout was mediated by active substance use, distinguishing direct protective and risk pathways.

---

## Key Findings

**Primary result:** Ambiguity tolerance did not predict subsequent opioid use at either temporal lag. Adding γ to clinical covariate models did not improve fit, suggesting this parameter does not carry prospective clinical signal at the individual level in this sample.

**Data quality as clinical signal:** Session exclusions were systematically associated with active substance use, elevated craving, sleep disturbance, and distress intolerance. Predictors of UTOX positivity and predictors of exclusion showed **distinct clinical profiles**, pointing to different pathways to vulnerability and data quality failure.

**Mediation:** Cognitive ability and positive affect were protective against dropout. Craving, sleep disturbance, and distress intolerance operated primarily **through active substance use** — consistent with drug-seeking behaviour disrupting study engagement.

Together, these findings argue that **missingness is a clinically informative endpoint** in dense-sampling designs, and that the distributional properties of retained data should not be assumed to represent the full clinical population.

The null prediction of γ on opioid use raises a deeper question: does ambiguity tolerance, as extracted from this paradigm, reflect a **stable individual trait with a neural substrate** — or is it more state-dependent, varying with clinical context? This question is directly addressed in a companion study using connectome-based predictive modelling in a healthy sample: [Whole-Brain Resting-State fMRI Prediction of Ambiguity Tolerance](/projects/4_project/).

---

## Code & Reproducibility

All analysis code is available at **[github.com/deng-hanwen/OUD_ambiguity_tolerance](https://github.com/deng-hanwen/OUD_ambiguity_tolerance)**, including R Markdown scripts for model fitting QC, logistic regression, propensity score weighting, mediation analysis, and visualisation. Raw data are not shared to protect participant confidentiality.

*MRes Dissertation, UCL / Yale University / Anna Freud Center. Supervised by Dr Sarah Yip & Dr Stephen Riley.*
