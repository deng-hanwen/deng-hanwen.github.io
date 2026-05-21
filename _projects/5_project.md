---
layout: page
title: Applied Psychometrics and Clinical Audit
description: Three collaborative projects in scale validation, cross-national survey analysis, and admissions equity — with reflections on what the null results reveal about design
img: assets/img/rob_thumb.png
importance: 1
category: Psychometric and Clinical Audit
related_publications: false
---

*Collaborative work with the [CORE Data Lab](https://www.thecoredatalab.com/), UCL Centre for Outcomes Research and Effectiveness. PI: Prof Rob Saunders.*

<p>
  <a href="https://github.com/deng-hanwen/COVID_AES_wellbeing" class="btn btn-sm z-depth-0" role="button" style="background-color: #424242; color: white; margin-right: 6px;">
    <i class="fab fa-github"></i> COVID-19 AES
  </a>
  <a href="https://github.com/deng-hanwen/HAS_UK_validation" class="btn btn-sm z-depth-0" role="button" style="background-color: #424242; color: white; margin-right: 6px;">
    <i class="fab fa-github"></i> HAS-UK
  </a>
  <a href="https://github.com/deng-hanwen/Dclinpsy_diversity" class="btn btn-sm z-depth-0" role="button" style="background-color: #424242; color: white;">
    <i class="fab fa-github"></i> DClinPsy
  </a>
</p>

---

## Overview

These three projects sit outside my primary research programme in computational psychiatry and neuroimaging. They are applied quantitative collaborations — secondary analyses and clinical audits where the main contribution was statistical modelling in R. The methods across all three draw from the same toolkit: confirmatory factor analysis (CFA), structural equation modelling (SEM), logistic regression, and measurement invariance testing.

What links them most usefully, in retrospect, is that all three produced null or inconclusive results — and the reasons why are informative about study design in applied clinical research.

---

## Study 1 — Psychometric Validation of the Hyperglycaemia Avoidance Scale UK

*Related publication: McKechnie et al. (2024), Diabetic Medicine.*

Adults with Type 1 diabetes sometimes tolerate high blood glucose (hyperglycaemia) to avoid the immediate danger of low blood glucose (hypoglycaemia). The HAS-UK measures this tendency across three proposed factors: Worry, Blood Glucose Decisions, and Lifestyle Decisions. The goal was to validate this factor structure in a UK clinical sample (*N* = 230) and test whether it measured the same construct equally across subgroups (measurement invariance by HbA1c level, age, hypoglycaemia history, and awareness status).

CFA was conducted using the WLSMV estimator in `lavaan` with ordered polytomous indicators. The three-factor model showed **poor fit** across all indices (CFI = 0.811, RMSEA = 0.115, SRMR = 0.131). Model estimation failed entirely for the high-HbA1c subgroup, precluding formal invariance testing.

**Reflection.** Imposing a confirmatory model before establishing the factor structure empirically is a well-recognised pitfall. The correct sequence is EFA on a development sample first — to let the data reveal dimensionality — then CFA on a holdout sample to confirm it. The modification indices revealed extensive cross-loadings and correlated residuals: the scale structure itself requires revision, not just validation in a new sample. Additionally, measurement invariance testing presupposes adequate model fit within each group; the workflow here had the steps inverted.

---

## Study 2 — COVID-19 Lockdown, Autonomy Experience, and Psychological Wellbeing

*Cross-national secondary analysis, N = 2,575 across 10 countries.*

This project examined how individuals' perceptions of COVID-19 lockdown policies related to psychological distress across 10 countries. The Autonomy Experience Scale (AES) captured three dimensions: Perceived Coercion (PC), Perceived Pressure (PP), and Procedural Justice (PJ). Outcomes were depression, anxiety, and stress (DASS-21). A two-level SEM (individual within country) tested whether AES components predicted distress via maladaptive coping, and whether between-country differences in AES scores could be explained by demographic aggregates, GDP, or lockdown stringency.

Within-country paths replicated sensibly across the full sample and a UK subsample. The between-country model was more complex: Perceived Coercion was negatively associated with coping between countries — opposite to the within-country direction — and the dominant source of country-level variance in AES scores remained unexplained.

**Reflection.** With only 10 countries, the Level 2 model was severely underpowered and underspecified from the outset. GDP and lockdown stringency capture little of what actually differs across countries in lockdown experience: government trust, prior experience of state authority, cultural norms around collective obligation, and specific policy communication were all unmeasured. A meaningful cross-national design would need to measure theoretically motivated country-level predictors directly, or restrict inference to within-country variation. The cross-level reversal in the PC coefficient is a textbook Simpson's paradox case — not a substantive finding, but a signal that the Level 2 model is missing key confounders.

---

## Study 3 — Demographic Equity Audit of DClinPsy Admissions

*2023 intake cohort, N = 1,140 applicants. 6.9% overall acceptance rate.*

The Doctorate in Clinical Psychology (DClinPsy) is the primary route to registration as a clinical psychologist in the UK. This project examined whether acceptance and rejection rates in the 2023 intake differed systematically across age, gender, ethnicity, disability, and sexual orientation, using logistic regression and Fisher's exact tests.

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/rob_dclinpsy_eth.png" alt="Bar chart of DClinPsy acceptance rates by ethnic group, 2023 intake" style="max-width: 70%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 1.</em> Acceptance rates by ethnic group (2023 intake). No group differences reached significance (Fisher's exact, p = .320). The overall rate of 6.9% creates severe base-rate constraints on statistical power within subgroups.</p>
</div>

Acceptance rates were broadly similar across groups. The only statistically significant predictor in the logistic regression was applicants aged 45–49 (OR ≈ 7.2, *p* = .013). No ethnic, disability, or sexual orientation group differences were significant.

**Reflection.** With a 7% overall acceptance rate, most demographic subgroups had too few acceptances to power any but very large effects. The null result here is not interpretable as evidence of equity — it is a power problem. The more appropriate design would be longitudinal: tracking acceptance patterns across multiple intake cohorts to detect drift, and pre-specifying the minimum detectable effect size at each subgroup's base rate before collecting data. A single cross-sectional snapshot of a small intake cohort cannot meaningfully address an equity question.

---

## What the Nulls Have in Common

Across all three studies, the null and inconclusive results shared a common structure: a mismatch between the question asked and the design used to answer it. A scale imposed on CFA before its structure was established. A cross-national model with ten countries and no theoretically motivated Level 2 predictors. A power analysis never conducted for a rare-event outcome in small demographic cells.

These are not failures of the phenomena — the underlying questions remain worth answering. They reflect constraints common in applied clinical research, where datasets are inherited rather than purpose-built and the pressure is to use available data rather than collect the right data. The practical lesson is that the statistical model should be scoped to what the data can actually support, not to what the research question ideally requires.

---

## Code

All analysis code is available as private repositories on GitHub: [COVID-19 AES Wellbeing](https://github.com/deng-hanwen/COVID_AES_wellbeing) · [HAS-UK Validation](https://github.com/deng-hanwen/HAS_UK_validation) · [DClinPsy Diversity](https://github.com/deng-hanwen/Dclinpsy_diversity). Participant data are not included.
