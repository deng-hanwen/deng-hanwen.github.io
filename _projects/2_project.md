---
layout: page
title: Neurobiological Markers of Opioid Use Disorder
description: Whole-brain functional connectivity analysis of OUD vs healthy controls using Network-Based Statistics across task and resting-state fMRI
img: assets/img/3.jpg
importance: 4
category: research
github: https://github.com/deng-hanwen/BrainStateDx-NBS
related_publications: false
---

<p>
  <a href="https://github.com/deng-hanwen/BrainStateDx-NBS" class="btn btn-sm z-depth-0" role="button" style="background-color: #424242; color: white;">
    <i class="fab fa-github"></i> View Code on GitHub
  </a>
</p>

> **Note:** This project is ongoing. Results presented here reflect analyses completed to date.

---

## Overview

Opioid Use Disorder (OUD) is associated with widespread alterations in brain function, yet it remains unclear whether these reflect **stable neurobiological trait markers** or transient, state-dependent disruptions. Resolving this distinction has direct implications for identifying diagnostic biomarkers versus treatment-sensitive targets.

This project examines whole-brain functional connectivity (FC) in OUD patients (n = 53) compared to healthy controls (n = 38) using fMRI data collected during two cognitive tasks — the Monetary Incentive Delay (MID) reward task and the Stroop cognitive control task — as well as resting-state. The primary questions are:

1. Are OUD–HC connectivity differences **consistent across task contexts**, or specific to particular cognitive demands?
2. Do connectivity differences represent **stable trait markers**, or are they modulated by treatment response?

---

## Methods

### Parcellation and Connectivity

Functional connectivity matrices were derived using the **268-node Shen atlas**, yielding a whole-brain connectome organised into 10 canonical functional networks (frontoparietal, default mode, motor, visual, salience, subcortical, cerebellar, and others). Connectivity was quantified as Fisher-z-transformed pairwise correlations.

### Network-Based Statistics (NBS)

Group differences in FC were tested using the **NBS toolbox** (Zalesky et al., 2010), a mass-univariate approach that controls family-wise error rate over edges by applying cluster-based inference over connected subgraphs of the connectome. Primary threshold: *t* = 3.1, 5,000 permutations, α = 0.05.

Four complementary analysis strategies were employed:

| Analysis | Approach |
|---|---|
| Per-task 2-sample *t*-test | Separate OUD vs HC comparisons within MID and Stroop |
| GLM with repeated measures | Full GLM testing group main effect and Dx × Task interaction across 182 observations |
| Averaged matrix *t*-test | Element-wise average of MID + Stroop per subject prior to testing |
| Conjunction analysis | Edges surviving NBS in **both** MID and Stroop independently |

A **repeated-measures NBR** approach extended the standard NBS to a within-subject design, with subject-level dummy variables and exchange blocks preserving the repeated-measures structure under permutation.

### Treatment Response Analysis

A subset of OUD participants with longitudinal outcome data were classified as responders vs non-responders based on urine toxicology confirmation. The diagnostic FC networks identified above were then tested as predictors of treatment response.

---

## Key Findings

The analyses reveal a consistent pattern: **OUD is characterised by large-scale FC alterations that are state-general rather than task-specific**.

The Dx × Task interaction was non-significant, while the group main effect was highly robust, with thousands of edges differentiating OUD from HC across both tasks. Conjunction analysis identified a core set of edges surviving independently in both MID and Stroop contexts — implying these differences do not depend on the cognitive demands of the task being performed.

Critically, the OUD–HC differences identified under task conditions **persisted in resting-state FC**, providing convergent evidence for a stable trait interpretation rather than a task-driven artefact. Key network hubs implicated in the OUD > HC direction include subcortical and frontoparietal nodes, consistent with circuits implicated in reward processing and cognitive control in the addiction literature.

However, these same diagnostic networks **did not predict treatment response**, suggesting a dissociation: the neural signature of OUD pathology and the neural correlates of recovery may reflect distinct biological processes.

---

## Code & Reproducibility

Analysis code is available at **[github.com/deng-hanwen/BrainStateDx-NBS](https://github.com/deng-hanwen/BrainStateDx-NBS)**, including MATLAB scripts for NBS analysis, conjunction and overlap analyses, and network-level summaries. Raw fMRI data are not shared due to participant confidentiality.

*Ongoing project. Yale University, Dr Sarah Yip.*
