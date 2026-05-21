---
layout: page
title: Neurobiological Markers of Opioid Use Disorder
description: Whole-brain Network-Based Statistics across reward and cognitive control fMRI tasks — probing the task-generality and clinical specificity of OUD functional connectivity
img: assets/img/nbs_thumb.png
importance: 4
category: Computational and Neuroimaging
github: https://github.com/deng-hanwen/BrainStateDx-NBS
related_publications: false
---

<p>
  <a href="https://github.com/deng-hanwen/BrainStateDx-NBS" class="btn btn-sm z-depth-0" role="button" style="background-color: #424242; color: white;">
    <i class="fab fa-github"></i> View Code on GitHub
  </a>
</p>

*Yale University. PI: Dr Sarah Yip. Dataset and foundational CPM analyses: Dr Sarah Lichenstein.*

> **Note:** This project is ongoing and currently in preparation. Specific results are not reported here.

---

## Overview

Two questions drive this project:

**Are functional connectivity differences between OUD patients and healthy controls task-specific, or do they reflect a stable, state-general neural signature of the disorder?**

**Do the FC networks that robustly distinguish OUD from healthy controls also predict who responds to treatment?**

These questions bear directly on the translational value of neuroimaging in addiction. If OUD-associated connectivity patterns are task-dependent artefacts, they offer limited utility as biomarkers. If they are stable, they constitute candidate trait markers of OUD pathology. But even a robust diagnostic signature may not track with clinical outcome: the network that best separates patients from controls need not be the network that predicts recovery.

The dataset is the same as Lichenstein et al. (2021, *Molecular Psychiatry*) — methadone-maintained individuals with OUD (*n* = 53) and healthy comparison participants (*n* = 38), scanned during two fMRI tasks: the Monetary Incentive Delay (MID) reward task and the Stroop cognitive control task, with a resting-state scan available for a subset (*n* = 36 OUD).

---

## Methods

### Parcellation and Connectivity

Functional connectivity matrices were derived using the **268-node Shen atlas**, organised into 10 canonical functional networks: medial frontal (MF), frontoparietal (FP), default mode (DMN), motor (Mot), visual I and II (VI, VII), visual association (VAs), salience (SAL), subcortical (SC), and cerebellar (CBL). Connectivity was quantified as Fisher-z-transformed pairwise Pearson correlations.

### Network-Based Statistics (NBS)

Group differences were tested using the **NBS toolbox** (Zalesky et al., 2010) — a mass-univariate approach that controls family-wise error rate by applying cluster-based inference over connected subgraphs of the connectome. All analyses used a primary threshold of *t* = 3.1 with 5,000 permutations at α = 0.05.

Four complementary analysis strategies were applied:

| Analysis | Design |
|---|---|
| Per-task 2-sample *t*-test | Separate OUD vs HC comparison within MID and Stroop |
| GLM with repeated measures | Full GLM testing group main effect and Dx × Task interaction across 182 observations, with within-subject exchange blocks |
| Averaged matrix *t*-test | Element-wise mean of MID + Stroop per subject → 2-sample *t*-test; the correct test of the Dx main effect |
| Conjunction | Edges surviving NBS independently in **both** MID and Stroop — the most conservative and replication-robust subset |

### Treatment Response

Participants were classified as **responders** (no opioid-positive urine screens during treatment; *n* = 19) or **non-responders** (*n* = 34) by urine toxicology. Mean FC at diagnostic network edges was compared between groups using Wilcoxon rank-sum tests, with healthy controls as a contextual reference.

---

## Research Direction

This project is examining two separable questions about functional connectivity (FC) in OUD: whether OUD–HC differences are consistent across task and resting-state contexts, and whether the networks that best distinguish patients from controls are the same as those that predict treatment response. These questions are conceptually distinct — a robust diagnostic signature and a clinically dynamic signature need not involve the same circuitry — and bear directly on how neuroimaging biomarkers in addiction should be interpreted and validated.

The analytic framework draws on prior work by Lichenstein et al. (2021), who applied connectome-based predictive modelling to the same dataset and identified a network predictive of opioid abstinence during treatment. That treatment-predictive network — characterised by within-network motor/sensory connectivity and connections spanning salience, default mode, and frontoparietal systems — provides an important reference point for interpreting any new NBS-derived diagnostic signatures.

<div style="text-align: center; margin: 2rem 0;">
  <a href="https://doi.org/10.1038/s41380-019-0586-y" target="_blank" rel="noopener">
    <img src="/assets/img/nbs_lich_fig3c.png" alt="Lichenstein 2021 Figure 3C: opioid abstinence network strength by treatment group" style="max-width: 55%; border: 1px solid #eee; padding: 6px;">
  </a>
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 1.</em> Opioid abstinence network strength by treatment group (Lichenstein et al., 2021; click to open paper). Network strength is highest in responders and lowest in non-responders, demonstrating that FC can track treatment outcome in this dataset. A key question in the present project is whether NBS-derived diagnostic networks show a comparable or dissociable pattern.</p>
</div>

Kurtin et al. (2026) report a parallel finding in an independent UK methadone sample, where OUD–HC connectivity differences showed a consistent pattern across cognitive and reward task contexts — supporting a trait-level interpretation of such diagnostic signatures. The present analyses are designed to test whether that pattern holds in this dataset and whether it extends to resting-state, and to examine its relationship with clinical outcome.

---

## Code & Reproducibility

Analysis code is available at **[github.com/deng-hanwen/BrainStateDx-NBS](https://github.com/deng-hanwen/BrainStateDx-NBS)**, including MATLAB scripts for NBS analysis, conjunction and averaged-matrix analyses, brain state comparison, and treatment response testing. Raw fMRI data are not shared due to participant confidentiality.

---

## References

Kurtin, D. L., Herlinger, K., Hayes, A., Hand, L., Fonville, L., Hill, R. G., Nutt, D. J., Lingford-Hughes, A. R., & Paterson, L. M. (2026). Task-related differences in network connectivity and dynamics in people with severe opioid use disorder compared with healthy controls. *Translational Psychiatry, 16*, 111.

Lichenstein, S. D., Scheinost, D., Potenza, M. N., Carroll, K. M., & Yip, S. W. (2021). Dissociable neural substrates of opioid and cocaine use identified via connectome-based modelling. *Molecular Psychiatry, 26*, 4383–4393.

Zalesky, A., Fornito, A., & Bullmore, E. T. (2010). Network-based statistic: Identifying differences in brain networks. *NeuroImage, 53*(4), 1197–1207.
