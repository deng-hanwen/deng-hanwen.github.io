---
layout: page
title: Applied Psychometrics and Clinical Audit
description: Three applied quantitative collaborations — scale validation, cross-national survey analysis, and admissions audit — spanning CFA, multilevel SEM, measurement invariance, and logistic regression
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

These three projects sit outside my primary research programme in computational psychiatry and neuroimaging. They are applied quantitative collaborations — secondary analyses and clinical audits where the main contribution was statistical modelling in R.

The methods across all three draw from the same toolkit: **confirmatory factor analysis (CFA)**, **structural equation modelling (SEM)**, **logistic regression**, and **measurement invariance testing**.

Across these projects, the practical value was in building fluency with the full pipeline of applied quantitative research in clinical psychology — from construct operationalisation through model selection to result interpretation. Working across an EFA-to-CFA validation programme, a two-level SEM with cross-cultural data, and a logistic regression audit exposed a set of conceptual tensions that are central to psychometrics more broadly: that measurement validity presupposes construct clarity; that cross-group comparison requires demonstrating, not assuming, measurement equivalence; that multilevel data structures create inferential constraints that cannot be resolved by model complexity alone; and that statistical power in rare-outcome clinical datasets needs to be scoped to the base rate before any analysis begins. These are not incidental difficulties — they are structural features of applied measurement that have directly shaped how I approach construct validity and latent variable modelling in my primary research programme.

---

## Study 1 — Psychometric Validation of the Hyperglycaemia Avoidance Scale UK

*Related publication: McKechnie et al. (2024), Diabetic Medicine.*

This project was something of a detour — taken before I had established a clear computational research identity. What it gave me was a grounding in applied psychometric methods: I came away with a working command of **CFA**, **measurement invariance testing**, **SEM**, and the practical decisions that go into scale validation work, all of which have since informed how I think about latent variable measurement more broadly.

Adults with Type 1 diabetes sometimes tolerate high blood glucose (hyperglycaemia) to avoid the immediate danger of low blood glucose (hypoglycaemia). The HAS-UK captures this tendency and was developed from a grounded theory model (McKechnie et al., 2023) identifying emotional overcontrol, perfectionism, and compulsive glucose monitoring as core mechanisms — structured around a feedback loop in which threat sensitivity, approach-focused coping, and diabetes technology interact to maintain hyperglycaemia aversion (see Figure 1 below). This project ran a full psychometric programme on a UK clinical sample (*N* = 230): **exploratory factor analysis (EFA)** to examine latent structure, **confirmatory factor analysis (CFA)** to test proposed models, **reliability analysis** (Cronbach's α and item-total correlations), and **convergent/divergent validity** testing against GAD-7, PHQ-9, PAID-5, and the Hypoglycaemia Fear Survey (HFS-II). Group comparisons and regression models examined associations with HbA1c, insulin modality, hypoglycaemia awareness, and severe hypoglycaemia history.

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/has_theoretical_model.png" alt="Theoretical model of the process of hyperglycaemia aversion, McKechnie et al. 2023" style="max-width: 90%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 1.</em> Theoretical model of the process of hyperglycaemia aversion (McKechnie et al., 2023, <em>British Journal of Health Psychology</em>). Control and high standards interact with threat sensitivity, difficulties tolerating discomfort, and approach-focused coping to produce the hyperglycaemia aversion profile; diabetes technology plays a reinforcing role throughout.</p>
</div>

**CFA** using the **WLSMV estimator** in `lavaan` showed poor fit for the proposed factor structure (CFI = 0.811, RMSEA = 0.115, SRMR = 0.131). Model estimation failed entirely for the high-HbA1c subgroup, precluding formal **measurement invariance** testing.

**Reflection.** The HAS-UK represents an important first step in quantifying hyperglycaemia aversion, but the construct remains conceptually and psychometrically developing. The original grounded theory paper explicitly acknowledges that hyperglycaemia aversion was "poorly described and defined" prior to that work, and that its sample was not representative — limiting the generalisability of the theoretical model. The validation paper itself flags unresolved issues: the "lifestyle decisions" subscale showed low internal consistency (α = .539), and the authors call for future work on test–retest reliability, sensitivity to change, and clinically meaningful cut-offs. These are not incidental limitations but reflections of a construct still in formation. The difficulties encountered here — factor instability, subgroup non-convergence, construct overlap with hypoglycaemia fear — should therefore be understood in that context: they reproduce tensions already present in the HAS-UK literature rather than arising from the analysis alone. Future work should treat HAS-UK scores as dimensional markers requiring further validation against behavioural, clinical, and longitudinal outcomes, rather than as definitive diagnostic indicators.

---

## Study 2 — COVID-19 Lockdown, Autonomy Experience, and Psychological Wellbeing

*Cross-national secondary analysis, N = 2,575 across 11 countries.*

This project examined how individuals' perceptions of COVID-19 lockdown policies related to psychological distress across 11 countries. The **Autonomy Experience Scale (AES)** captured three dimensions: Perceived Coercion (PC), Perceived Pressure (PP), and Procedural Justice (PJ). Outcomes were depression, anxiety, and stress (**DASS-21**).

Analysis proceeded in stages. **Linear regression** first examined individual-level predictors of perceived coercion — demographics, income loss, caring responsibilities, and self-reported psychiatric diagnoses. The nested structure of the data (individuals within countries) then called for **linear mixed-effects models (LME)**, implemented in `lme4`. A key design decision concerned whether to specify country as a **fixed** or **random effect**: with only 11 Level-2 clusters, random-effects estimation is generally underpowered, but the substantive interest in country-specific differences argued for fixed-effect specification. **Estimated marginal means (EMMs)** were used to derive adjusted country-level means with confidence intervals, enabling covariate-controlled cross-national comparison. A **two-level SEM** then tested whether AES components predicted distress via maladaptive coping, and whether residual between-country variance in AES scores was accounted for by GDP or lockdown stringency.

Country membership was the strongest predictor of perceived coercion (OLS R² = .276), with substantial variation across countries. Within-country paths were consistent: PP and PJ predicted maladaptive coping, which in turn strongly predicted depression (β = .49) and anxiety (β = .45). Between-country variance in AES scores remained largely unexplained by the available country-level predictors.

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/rob_covid_pc.png" alt="Estimated marginal means of perceived coercion by country" style="max-width: 55%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 2.</em> Estimated marginal means (±SE) of Perceived Coercion by country (OLS, UK reference). Argentina and Italy showed the highest perceived coercion; Pakistan and Turkey the lowest. Country explained 27.6% of variance in PC — the strongest country-level effect across all six outcomes.</p>
</div>

**Reflection.** Three structural limitations constrained what this project could establish.

*Measurement equivalence across cultures.* Between-country comparison of raw AES scores presupposes that perceived coercion is psychometrically equivalent across national contexts. This assumption warrants formal testing: individuals in different political and institutional environments may interpret items concerning governmental restriction, personal autonomy, and procedural legitimacy through qualitatively different frameworks. The appropriate methodological approach would have been to test **measurement invariance** sequentially (configural → metric → scalar) prior to cross-national comparison (Putnick & Bornstein, 2016). Without this, observed country differences in PC scores cannot be unambiguously attributed to true differences in perceived coercion rather than to differential item functioning. That this limitation is consequential is evident from the cross-cultural DASS-21 literature, where full scalar invariance across national groups frequently fails (Putnick & Bornstein, 2016), suggesting that even well-validated instruments cannot be assumed equivalent across populations without empirical verification.

*Country as a composite predictor.* Country membership accounted for 27.6% of variance in perceived coercion, yet country simultaneously indexes lockdown stringency, government trust, economic instability, COVID-19 mortality, and cultural orientation. Specifying country as a categorical predictor conflates these pathways and precludes their disaggregation. Inclusion of theoretically motivated country-level covariates — including the Oxford COVID-19 Government Response Stringency Index (Hale et al., 2021) and institutional trust indices (Devine et al., 2021) — would have enabled partial decomposition of the between-country variance rather than leaving it as an uninterpreted residual. Evidence that cultural tightness–looseness independently predicts cross-national variation in COVID-related outcomes (Gelfand et al., 2021) further indicates that such dimensions should be formally specified rather than absorbed into a country dummy. The cross-level reversal in the PC path (negative between-country, positive within-country) signals residual confounding at Level 2 that the available predictors were insufficient to identify.

*Temporal ambiguity.* The cross-sectional design does not permit inference about the directionality of the coercion–distress association. Pre-existing psychological distress may inflate perceived coercion, perceived coercion may exacerbate distress, or both may reflect shared antecedents including prior mental health history or socioeconomic vulnerability. A longitudinal design with repeated assessment across discrete lockdown phases — policy tightening, reopening, vaccine rollout — would have been necessary to establish temporal precedence and to determine whether coercion perceptions track policy changes or are primarily driven by stable individual-difference factors.

The substantial unexplained between-country variance in perceived coercion — not accounted for by GDP or objective policy stringency — is consistent with evidence that institutional trust (Devine et al., 2021) and cultural orientation (Gelfand et al., 2021) independently moderate population responses to restriction policies. These constructs should be treated as primary moderators in future cross-national designs rather than residual sources of between-country noise.

#### References

Devine, D., Gaskell, J., Jennings, W., & Stoker, G. (2021). Trust and the coronavirus pandemic: What are the consequences of and for trust? *Political Studies Review, 19*(2), 274–285.

Gelfand, M. J., Jackson, J. C., Pan, X., Nau, D., Pieper, D., Denison, E., Dagher, M., Van Lange, P. A. M., Chiu, C., & Wang, M. (2021). The relationship between cultural tightness–looseness and COVID-19 cases and deaths: a global analysis. *The Lancet Planetary Health, 5*(3), e135–e144.

Hale, T., Angrist, N., Goldszmidt, R., Kira, B., Petherick, A., Phillips, T., Webster, S., Cameron-Blake, E., Hallas, L., Majumdar, S., & Tatlow, H. (2021). A global panel database of pandemic policies (Oxford COVID-19 Government Response Tracker). *Nature Human Behaviour, 5*, 529–538.

Putnick, D. L., & Bornstein, M. H. (2016). Measurement invariance conventions and reporting: The state of the art and future directions for psychological research. *Developmental Review, 41*, 71–90.

---

## Study 3 — Demographic Equity Audit of DClinPsy Admissions

*2023 intake cohort, N = 1,140 applicants. 6.9% overall acceptance rate.*

The Doctorate in Clinical Psychology (DClinPsy) is the primary route to registration as a clinical psychologist in the UK. This project was conducted in collaboration with a London university as part of an internal equity and diversity audit, with the analysis intended for inclusion in the programme's formal diversity report. It examined whether acceptance rates in the 2023 intake differed systematically across age, gender, ethnicity, disability, and sexual orientation, using **logistic regression** and **Fisher's exact tests**.

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/rob_dclinpsy_eth.png" alt="Bar chart of DClinPsy acceptance rates by ethnic group, 2023 intake" style="max-width: 55%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 3.</em> Acceptance rates by ethnic group (2023 intake). The dashed line indicates the overall acceptance rate (6.9%). No between-group differences were statistically significant.</p>
</div>

Acceptance rates were broadly similar across demographic groups. The only statistically significant predictor in the **logistic regression** was applicants aged 45–49 (OR ≈ 7.2, *p* = .013). No ethnic, disability, or sexual orientation group differences were significant.

---

## Code

All analysis code is available as private repositories on GitHub: [COVID-19 AES Wellbeing](https://github.com/deng-hanwen/COVID_AES_wellbeing) · [HAS-UK Validation](https://github.com/deng-hanwen/HAS_UK_validation) · [DClinPsy Diversity](https://github.com/deng-hanwen/Dclinpsy_diversity). Participant data are not included.
