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

*Yale University. Dr Sarah Yip.*

> **Note:** This project is ongoing. Results presented here reflect analyses completed to date.

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

## Key Findings

### OUD–HC differences are large-scale and robust across tasks

The per-task analyses identified large, highly significant OUD–HC differences in both directions:

- **MID:** OUD > HC: 175 edges (*p* < 0.0001); HC > OUD: 84 edges (*p* = 0.0016)
- **Stroop:** OUD > HC: 184 edges (*p* < 0.0001); HC > OUD: 230 edges (*p* < 0.0001)

Averaging matrices across tasks yielded the most sensitive result: **242 OUD > HC edges** and **237 HC > OUD edges** (both *p* < 0.0002, single components). The Dx × Task interaction was non-significant (*p* = 0.069), confirming that OUD-associated connectivity alterations do not depend on task context. The 27 OUD > HC and 28 HC > OUD conjunction edges (surviving NBS in **both** tasks independently) overlapped 100% with the averaged network, validating cross-task replication in the most conservative sense.

### Network anatomy

The **OUD > HC** network is dominated by subcortical-cortical hyperconnectivity. The highest-degree hub is a right subcortical node (degree 58), with the densest connections spanning frontoparietal–motor (FP↔Mot), frontoparietal–subcortical (FP↔SC), and subcortical–visual association (SC↔VAs) circuits.

The **HC > OUD** network is characterised by motor and cerebellar connectivity, with the top hub in the left cerebellum (degree 24) and the leading pairs within-motor (Mot↔Mot), cerebellar–motor (CBL↔Mot), and motor–subcortical (Mot↔SC).

### FC differences are state-general

The OUD–HC group difference at MID-identified edges is fully preserved during the Stroop task and vice versa, and the directional pattern extends into resting-state. This holds across all four edge sets.

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/nbs_brainstate.png" alt="Bar plots showing mean FC at per-task NBS edges across MID, Stroop, and resting-state for OUD and HC" style="max-width: 95%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 1.</em> Mean FC (Fisher-z, ± SE) at per-task NBS edges across brain states. Each panel shows OUD (salmon) and HC (blue) at edges identified by MID or Stroop NBS, evaluated during MID task, Stroop task, and OUD resting-state. The group difference is preserved across all brain states. HC resting-state data unavailable (n/a); OUD rest n = 36.</p>
</div>

### Diagnostic networks do not predict treatment response

Despite their robustness, these diagnostic networks showed **no significant association with treatment response** (all *p* = 0.22–0.98). Strikingly, the direction was *opposite* to what a normalisation hypothesis would predict: responders sat *further* from healthy controls than non-responders at every edge set. Both OUD subgroups remained far from healthy connectivity levels.

---

## Discussion

The findings point to a **dissociation between two distinct neural signatures** of OUD: a large-scale, state-general diagnostic signature that separates patients from controls across task and rest contexts, and a clinically dynamic signature that tracks treatment outcome — which is not the diagnostic network.

Lichenstein et al. (2021) applied CPM to the same dataset and identified a network predictive of opioid abstinence during treatment (*r* = 0.32, *p* = 0.018 from Stroop data). That opioid abstinence network is characterised predominantly by within-network motor/sensory connectivity and by connections between motor/sensory, salience, default mode, and frontoparietal networks — anatomically distinct from the subcortical-cortical hyperconnectivity that dominates the diagnostic NBS results here.

The figures below capture both sides of this dissociation: the left shows that network strength on the **treatment-predictive network** cleanly separates responders from controls from non-responders; the right shows that on the **diagnostic network**, both OUD subgroups sit far above healthy controls, with no meaningful separation between responders and non-responders.

<div style="text-align: center; margin: 2rem 0;">
  <div style="display: inline-flex; gap: 2rem; justify-content: center; align-items: flex-start; flex-wrap: wrap;">
    <div style="max-width: 340px;">
      <img src="/assets/img/nbs_lich_fig3c.png" alt="Lichenstein 2021 Figure 3C: opioid abstinence network strength by treatment group" style="width: 100%; border: 1px solid #eee; padding: 6px;">
      <p style="font-size: 0.82em; color: #666; margin-top: 0.4rem; text-align: left;"><strong>Treatment-predictive network</strong> (Lichenstein et al., 2021). Opioid abstinence network strength (y-axis) is highest in responders, intermediate in healthy controls, and lowest in non-responders. The network tracks recovery.</p>
    </div>
    <div style="max-width: 500px;">
      <img src="/assets/img/nbs_analysis12.png" alt="Analysis 12: diagnostic NBS network strength by treatment group, showing no separation" style="width: 100%; border: 1px solid #eee; padding: 6px;">
      <p style="font-size: 0.82em; color: #666; margin-top: 0.4rem; text-align: left;"><strong>Diagnostic network</strong> (this study). Mean FC at OUD–HC conjunction edges does not differentiate responders from non-responders (all *p* > .19). Both OUD groups remain far from healthy control levels — the diagnostic signature is fixed, not clinically dynamic.</p>
    </div>
  </div>
  <p style="font-size: 0.82em; color: #666; margin-top: 0.8rem;"><em>Figure 2.</em> Dissociation between treatment-predictive and diagnostic FC networks. Left panel reproduced from Lichenstein et al. (2021).</p>
</div>

This distinction matters for biomarker research in addiction. Stable diagnostic FC markers may index fixed neurobiological consequences of chronic opioid exposure and are relevant for understanding disorder mechanisms — but they should not be assumed to be appropriate targets for tracking clinical change. Kurtin et al. (2026) report a parallel finding in an independent UK methadone sample, where OUD–HC connectivity differences showed a consistent pattern across cognitive and reward task contexts, supporting a trait-level rather than state-specific interpretation.

---

## Code & Reproducibility

Analysis code is available at **[github.com/deng-hanwen/BrainStateDx-NBS](https://github.com/deng-hanwen/BrainStateDx-NBS)**, including MATLAB scripts for NBS analysis, conjunction and averaged-matrix analyses, brain state comparison, and treatment response testing. Raw fMRI data are not shared due to participant confidentiality.

---

## References

Kurtin, D. L., Herlinger, K., Hayes, A., Hand, L., Fonville, L., Hill, R. G., Nutt, D. J., Lingford-Hughes, A. R., & Paterson, L. M. (2026). Task-related differences in network connectivity and dynamics in people with severe opioid use disorder compared with healthy controls. *Translational Psychiatry, 16*, 111.

Lichenstein, S. D., Scheinost, D., Potenza, M. N., Carroll, K. M., & Yip, S. W. (2021). Dissociable neural substrates of opioid and cocaine use identified via connectome-based modelling. *Molecular Psychiatry, 26*, 4383–4393.

Zalesky, A., Fornito, A., & Bullmore, E. T. (2010). Network-based statistic: Identifying differences in brain networks. *NeuroImage, 53*(4), 1197–1207.
