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

1. **Are functional connectivity (FC) differences between OUD patients and healthy controls task-specific — tied to the demands of a particular cognitive context — or do they reflect a stable, state-general neural signature of the disorder?**
2. **Do the FC networks that robustly distinguish OUD from healthy controls also predict who responds to methadone treatment?**

These questions bear directly on the translational value of neuroimaging in addiction. If OUD-associated connectivity patterns are task-dependent artefacts, they offer limited utility as biomarkers. If they are stable, they constitute candidate trait markers of OUD pathology. But even a robust diagnostic signature may not track with clinical outcome: the network that best separates patients from controls need not be the network that predicts recovery.

The dataset used here is the same as that in Lichenstein et al. (2021, *Molecular Psychiatry*) — methadone-maintained individuals with OUD (*n* = 53) and healthy comparison participants (*n* = 38), scanned during two fMRI tasks: the Monetary Incentive Delay (MID) reward task and the Stroop cognitive control task, with a subset (*n* = 36 OUD) also providing resting-state data.

---

## Methods

### Parcellation and Connectivity

Functional connectivity matrices were derived using the **268-node Shen atlas**, organised into 10 canonical functional networks: medial frontal (MF), frontoparietal (FP), default mode (DMN), motor (Mot), visual I and II (VI, VII), visual association (VAs), salience (SAL), subcortical (SC), and cerebellar (CBL). Connectivity was quantified as Fisher-z-transformed pairwise Pearson correlations.

### Network-Based Statistics (NBS)

Group differences were tested using the **NBS toolbox** (Zalesky et al., 2010) — a mass-univariate approach that controls family-wise error rate by applying cluster-based inference over connected subgraphs of the connectome. All analyses used: primary threshold *t* = 3.1, 5,000 permutations, α = 0.05.

Four complementary analysis strategies were applied:

| Analysis | Design |
|---|---|
| Per-task 2-sample *t*-test | Separate OUD vs HC comparison within MID and Stroop |
| GLM with repeated measures | Full GLM testing group main effect and Dx × Task interaction across 182 observations (91 subjects × 2 tasks), with within-subject exchange blocks |
| Averaged matrix *t*-test | Element-wise mean of MID + Stroop matrices per subject, then 2-sample *t*-test — the correct test of the group main effect under the repeated-measures structure |
| Conjunction analysis | Edges surviving NBS independently in **both** MID and Stroop — the most statistically conservative and replication-robust subset |

### Treatment Response Analysis

Participants were classified as **responders** (no opioid-positive urine screens during treatment; *n* = 19) or **non-responders** (*n* = 34) based on urine toxicology. Mean FC at diagnostic network edges was compared between groups using Wilcoxon rank-sum tests, with healthy controls shown as a contextual reference.

---

## Key Findings

### 1. OUD–HC connectivity differences are large-scale and robustly bilateral

The per-task analyses identified large, highly significant OUD–HC differences in both directions:

- **MID:** OUD > HC: 175 edges (*p* < 0.0001); HC > OUD: 84 edges (*p* = 0.0016)
- **Stroop:** OUD > HC: 184 edges (*p* < 0.0001); HC > OUD: 230 edges (*p* < 0.0001)

Averaging matrices across the two tasks and running a single 2-sample *t*-test — the appropriate test of the Dx main effect — yielded the most sensitive result: **242 OUD > HC edges** and **237 HC > OUD edges** (both *p* < 0.0002, single components). The Dx × Task interaction was non-significant (*p* = 0.069), indicating that OUD-associated connectivity alterations do not depend on task context.

The 27 OUD > HC and 28 HC > OUD edges surviving conjunction (present independently in **both** MID and Stroop NBS) overlapped 100% with the averaged NBS network, validating cross-task replication in the most conservative possible sense.

### 2. Network anatomy: subcortical hyperconnectivity and cerebellar hypoconnectivity

The OUD > HC network is dominated by **subcortical-cortical hyperconnectivity**. The highest-degree hub is a right subcortical node (degree 58 in the averaged network), with the densest inter-network connections spanning frontoparietal–motor (FP↔Mot), frontoparietal–subcortical (FP↔SC), and subcortical–visual association (SC↔VAs) circuits.

The HC > OUD network (edges where controls show higher FC than OUD) is characterised by **motor and cerebellar connectivity**, with the highest-degree hub in the left cerebellum (degree 24) and the top pairs within-motor (Mot↔Mot), cerebellar–motor (CBL↔Mot), and motor–subcortical (Mot↔SC).

### 3. FC differences are state-general — they persist across tasks and into rest

The critical test of task-dependence was to extract mean FC at task-identified network edges *across brain states*. As shown below, the OUD–HC group difference at MID-identified edges is fully preserved during the Stroop task (and vice versa), and extends directionally into resting-state. The qualitative pattern holds across all four edge sets (MID OUD>HC, MID HC>OUD, Stroop OUD>HC, Stroop HC>OUD).

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/nbs_brainstate.png" alt="Bar plots showing mean FC at per-task NBS edges across MID, Stroop, and resting-state brain states for OUD and HC groups" style="max-width: 95%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 1.</em> Mean FC (Fisher-z, ± SE) at per-task NBS-identified edges across brain states. Each panel shows OUD (salmon) and HC (blue) at edges identified by MID or Stroop NBS, evaluated during MID task, Stroop task, and OUD resting-state. The directional group difference is preserved across all brain states, indicating state-generality rather than task-driven artefact. HC resting-state data were unavailable in this dataset (n/a). Resting-state data available for n = 36 OUD.</p>
</div>

The violin plots below show the same pattern at the conjunction edges — the statistically most robust subset — revealing consistent separation between OUD and HC across MID, Stroop, and rest at the individual level.

<div style="text-align: center; margin: 2rem 0;">
  <img src="/assets/img/nbs_violin_conjunction.png" alt="Violin plots of mean FC at conjunction edges (OUD > HC and HC > OUD) across MID, Stroop, and resting-state brain states" style="max-width: 80%; border: 1px solid #eee; padding: 8px;">
  <p style="font-size: 0.85em; color: #666; margin-top: 0.5rem;"><em>Figure 2.</em> Distribution of individual mean FC at conjunction edges across brain states. Top: 27 OUD > HC edges; Bottom: 28 HC > OUD edges. Orange = OUD (*n* = 53 for task, *n* = 36 for rest); Blue = HC (*n* = 38; resting-state n/a). Median shown by horizontal line. The between-group separation is consistent across both tasks and resting-state.</p>
</div>

### 4. Diagnostic networks do not predict treatment response

Despite the robustness of OUD–HC connectivity differences, these same networks showed **no significant association with treatment response** across all edge sets tested (all *p* = 0.22–0.98 by Wilcoxon rank-sum). Critically, the direction of the (non-significant) effect was *opposite* to what a normalisation hypothesis would predict: treatment responders sat *further* from healthy controls than non-responders, not closer. At OUD > HC edges, responders showed the highest connectivity (responder > non-responder > HC); at HC > OUD edges, responders showed the lowest (HC > non-responder > responder). Both OUD subgroups remained far from healthy levels.

---

## Discussion

The pattern of findings points to a **dissociation between two distinct neural signatures** in OUD: a large-scale, state-general diagnostic signature that distinguishes patients from healthy controls across task and rest contexts, and a clinically dynamic signature that tracks with treatment outcome — which is not the diagnostic network.

This dissociation is directly supported by Lichenstein et al. (2021), who applied CPM to the same dataset to identify a network predictive of opioid abstinence during treatment (*r* = 0.32, *p* = 0.018 from Stroop data; MID failed). That opioid abstinence network consisted predominantly of within-network motor/sensory connections and connectivity between motor/sensory, salience, default mode, and frontoparietal networks — a profile anatomically distinct from the subcortical-cortical hyperconnectivity that dominates our diagnostic NBS results. The complementary finding is therefore: the networks that separate OUD from controls do not predict recovery, and the network that predicts recovery does not systematically separate OUD from controls.

This distinction matters for translational research. Stable diagnostic FC markers may index fixed neurobiological consequences of chronic opioid exposure — potentially relevant as inclusion criteria or for understanding disorder mechanisms — but should not be assumed to be appropriate targets for outcome-tracking or treatment response prediction. Kurtin et al. (2026) report a parallel finding in an independent UK methadone sample: connectivity differences between patients and healthy controls during MID and cue reactivity tasks showed a broadly consistent pattern across task conditions, supporting the interpretation of these alterations as trait-level characteristics of methadone-maintained individuals rather than state-specific disruptions.

An important caveat: the current treatment response analysis used a binary outcome (responder/non-responder during treatment). The CPM in Lichenstein et al. (2021) used a continuous measure (% opioid-negative urines), which provides substantially greater sensitivity. Whether continuous abstinence measures would reveal a weak relationship with diagnostic network strength in the current dataset remains an open question.

---

## Code & Reproducibility

Analysis code is available at **[github.com/deng-hanwen/BrainStateDx-NBS](https://github.com/deng-hanwen/BrainStateDx-NBS)**, including MATLAB scripts for NBS analysis, conjunction and averaged-matrix analyses, brain state comparison, and treatment response testing. Raw fMRI data are not shared due to participant confidentiality.

---

## References

Kurtin, D. L., Herlinger, K., Hayes, A., Hand, L., Fonville, L., Hill, R. G., Nutt, D. J., Lingford-Hughes, A. R., & Paterson, L. M. (2026). Task-related differences in network connectivity and dynamics in people with severe opioid use disorder compared with healthy controls. *Translational Psychiatry, 16*, 111.

Lichenstein, S. D., Scheinost, D., Potenza, M. N., Carroll, K. M., & Yip, S. W. (2021). Dissociable neural substrates of opioid and cocaine use identified via connectome-based modelling. *Molecular Psychiatry, 26*, 4383–4393.

Zalesky, A., Fornito, A., & Bullmore, E. T. (2010). Network-based statistic: Identifying differences in brain networks. *NeuroImage, 53*(4), 1197–1207.
