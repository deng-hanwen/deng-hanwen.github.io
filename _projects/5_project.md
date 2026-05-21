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

These three projects sit outside my primary research programme in computational psychiatry and neuroimaging. They are applied quantitative collaborations — secondary analyses and clinical audits where the main contribution was statistical modelling in R. The methods across all three draw from the same toolkit: **confirmatory factor analysis (CFA)**, **structural equation modelling (SEM)**, **logistic regression**, and **measurement invariance testing**.

What links them most usefully, in retrospect, is that all three produced null or inconclusive results — and the reasons why are informative about the limits of the methods in applied clinical research settings.

---

## Study 1 — Psychometric Validation of the Hyperglycaemia Avoidance Scale UK

*Related publication: McKechnie et al. (2024), Diabetic Medicine.*

Adults with Type 1 diabetes sometimes tolerate high blood glucose (hyperglycaemia) to avoid the immediate danger of low blood glucose (hypoglycaemia). The HAS-UK measures this tendency across three proposed factors: Worry, Blood Glucose Decisions, and Lifestyle Decisions. The goal was to validate this factor structure in a UK clinical sample (*N* = 230) and test whether it measured the same construct equally across clinical subgroups — **measurement invariance** by HbA1c level, age, hypoglycaemia history, and awareness status.

**CFA** was conducted using the **WLSMV estimator** in `lavaan` with ordered polytomous indicators. The three-factor model showed **poor fit** across all indices (CFI = 0.811, RMSEA = 0.115, SRMR = 0.131). Model estimation failed entirely for the high-HbA1c subgroup, precluding formal invariance testing.

**Reflection.** The poor fit did not reflect an error in the analysis pipeline — the CFA model faithfully implemented the factor structure established in the original scale development. Rather, it suggests the HAS-UK items may function differently in a UK clinical sample than in the population for which the scale was originally developed. The WLSMV estimator with ordered polytomous indicators also requires adequate cell frequencies across response categories; sparse responses on some items reduced the effective information available for estimation. Most consequentially, the non-convergence of the high-HbA1c subgroup model meant that the most clinically interesting comparison — whether the scale measures hyperglycaemia avoidance equivalently in well-controlled versus poorly-controlled diabetes — simply could not be answered with the available data. Measurement invariance testing presupposes a model that fits in each group individually, and that baseline condition was not met.

---

## Study 2 — COVID-19 Lockdown, Autonomy Experience, and Psychological Wellbeing

*Cross-national secondary analysis, N = 2,575 across 10 countries.*

This project examined how individuals' perceptions of COVID-19 lockdown policies related to psychological distress across 10 countries. The **Autonomy Experience Scale (AES)** captured three dimensions: Perceived Coercion (PC), Perceived Pressure (PP), and Procedural Justice (PJ). Outcomes were depression, anxiety, and stress (**DASS-21**). A **two-level SEM** (individual within country) tested whether AES components predicted distress via maladaptive coping, and whether between-country differences in AES scores could be explained by demographic aggregates, GDP, or lockdown stringency.

Country membership was the strongest predictor of perceived coercion (OLS R² = .276), with substantial variation across the 10 countries. Within-country paths were consistent: PP and PJ predicted maladaptive coping, which in turn strongly predicted depression (β = .49) and anxiety (β = .45). Between-country variance in AES scores, however, remained largely unexplained by the available country-level predictors.

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/rob_covid_pc.jpg" alt="Estimated marginal means of perceived coercion by country" style="max-width: 80%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 1.</em> Estimated marginal means (±SE) of Perceived Coercion by country (OLS, UK reference). Argentina and Italy showed the highest perceived coercion; Pakistan and Turkey the lowest. Country explained 27.6% of variance in PC — the strongest country-level effect across all six outcomes.</p>
</div>

**Reflection.** The within-country findings were coherent and consistent with the theoretical model. The between-country model was the more ambitious question, and the available country-level predictors — GDP and lockdown stringency index — captured little of what actually differed across countries in how lockdowns were experienced. Government trust, prior experience of state authority, and cultural norms around collective obligation were all unmeasured. With only 10 countries at Level 2, the **multilevel SEM** also had minimal degrees of freedom for testing country-level effects, making the null at that level difficult to interpret. The cross-level reversal in the PC path (negative between-country, positive within-country) signals a confounding structure at Level 2 that the model was not equipped to identify.

---

## Study 3 — Demographic Equity Audit of DClinPsy Admissions

*2023 intake cohort, N = 1,140 applicants. 6.9% overall acceptance rate.*

The Doctorate in Clinical Psychology (DClinPsy) is the primary route to registration as a clinical psychologist in the UK. This project examined whether acceptance and rejection rates in the 2023 intake differed systematically across age, gender, ethnicity, disability, and sexual orientation, using **logistic regression** and **Fisher's exact tests**.

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/rob_dclinpsy_eth.png" alt="Bar chart of DClinPsy acceptance rates by ethnic group, 2023 intake" style="max-width: 70%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 2.</em> Acceptance rates by ethnic group (2023 intake). No group differences were statistically significant. The overall acceptance rate of 6.9% creates severe base-rate constraints on statistical power within subgroups.</p>
</div>

Acceptance rates were broadly similar across demographic groups. The only statistically significant predictor in the **logistic regression** was applicants aged 45–49 (OR ≈ 7.2, *p* = .013). No ethnic, disability, or sexual orientation group differences were significant.

**Reflection.** With a 7% overall acceptance rate, most demographic subgroups had too few acceptances to detect anything but very large effects — the study was structurally underpowered for its question. The null result is therefore not interpretable as evidence of equity. A more informative design would track acceptance patterns longitudinally across multiple intake cohorts to detect drift, and pre-specify the minimum detectable effect size at each subgroup's base rate before data collection. A single cross-sectional snapshot of a small intake cohort cannot meaningfully address a fairness question.

---

## What the Nulls Have in Common

Across all three studies, the inconclusive results shared a common structure: methods that were appropriate in principle ran into data constraints that limited what they could resolve. A **CFA** that could not converge in the most clinically important subgroup. A **multilevel SEM** with too few Level 2 units to model between-country structure adequately. A **logistic regression** applied to an outcome too rare to power meaningful subgroup comparisons.

These reflect constraints common in applied clinical research, where datasets are inherited rather than purpose-built. The practical lesson is not that the methods were wrong, but that the inferential goals need to be scoped honestly to what the data can support.

---

## Code

All analysis code is available as private repositories on GitHub: [COVID-19 AES Wellbeing](https://github.com/deng-hanwen/COVID_AES_wellbeing) · [HAS-UK Validation](https://github.com/deng-hanwen/HAS_UK_validation) · [DClinPsy Diversity](https://github.com/deng-hanwen/Dclinpsy_diversity). Participant data are not included.
