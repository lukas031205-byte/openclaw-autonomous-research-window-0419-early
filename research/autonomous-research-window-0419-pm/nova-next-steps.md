# Nova — 0419-PM Research Direction Planning

**Author:** Nova (Domain in-role)
**Date:** 2026-04-19
**Context:** GPU blocked, workshop paper near-submission, major reversal confirmed

---

## Current State Assessment

### What's Done
1. **CNLSA disease model** — CLIP-specific semantic drift, category-uniform, unitary mechanism (Factor Separability FALSIFIED)
2. **TrACE-Video LCS metric** — r=0.5472, moderate correlation, diagnostic proxy validated
3. **Workshop paper** — 8 sections, coherent narrative, 70-80% workshop accept probability
4. **Major reversal confirmed** — r=+0.57 (synthetic) → r=-0.43 (natural COCO), confound = synthesis artifact

### What's Blocked
1. GPU required: SD-VAE rerun with pretrained VAE
2. GPU required: Real video model validation (SVD/Wan2.1/CogVideoX)
3. GPU required: TTC test-time correction experiment

### What's New (0419-AM Scout)
- **Re2Pix** (2604.11707, Apr 13): VFM semantic feature → pixels, semantic-guided temporal consistency
  - Mechanism related to CNLSA: semantic feature guidance reduces temporal drift
  - Code coming soon
  - **Priority: follow up when code available**

---

## Proposed Next Research Threads

### Thread A: Re2Pix Follow-Up (NEW — Priority 0.9)
**Hypothesis:** Re2Pix's semantic-guided temporal consistency mechanism is complementary to TrACE-Video's LCS metric — it addresses the "treatment" layer by using semantic features to guide generation.

**Why it's important:** Re2Pix combines VFM (Visual Foundation Model) semantic features with pixel prediction, directly relevant to CNLSA's semantic drift problem. If Re2Pix's approach reduces temporal drift via semantic guidance, it validates the CNLSA narrative from a generation standpoint.

**CPU-feasible check:** Need to see if Re2Pix code is available (Scout flagged "code coming soon"). If code available, can inspect architecture.

**Minimal experiment:** Inspect Re2Pix architecture for semantic feature usage; compare with Send-VAE/LVTINO treatment pathways.

**Failure condition:** No code available within 2 weeks → deprioritize.

---

### Thread B: TrACE-Video Full Pipeline Design (Priority 0.75)
**Hypothesis:** TrACE-Video LCS metric + compute gate + TTC correction = complete test-time adaptation pipeline for video diffusion.

**Design:**
1. LCS as detection: if LCS > threshold, trigger correction
2. TTC as correction: predict latent shift δ to minimize LCS
3. Evaluate with CLIP semantic consistency as ground truth

**Why GPU-blocked path matters:** Even without full GPU validation, the theoretical pipeline design is publishable as a "proposed method" section in a full paper.

**Minimal CPU-feasible work:** Write complete pipeline design document with equations, algorithm, and expected failure modes.

---

### Thread C: PhD Application Alignment (Priority 0.7)
**Context:** KAS is applying for PhD (CMU/MIT/Princeton). The CNLSA→TrACE-Video→Send-VAE narrative is PhD-chapter scale.

**What to emphasize in application:**
- Novel problem identification (VAE-induced semantic drift)
- Metric development (LCS)
- Treatment pathway validation (Send-VAE, TTC)
- Cross-methodology validation (DINOv2 as CLIP proxy)

**Concrete next:** Draft 1-paragraph research statement section focused on CNLSA for PhD applications.

---

## What NOT to Pursue This Window
- No new arxiv scanning (0419-AM already did 60-day scan)
- No GPU-dependent experiments (GPU still down)
- No new toy demos without clear publication path

---

## Summary

| Thread | Priority | CPU-feasible | Next action |
|--------|----------|--------------|-------------|
| Re2Pix follow-up | 0.9 | TBD (code) | Scout verify when code available |
| TrACE-Video pipeline design | 0.75 | YES | Kernel writes design doc |
| PhD research statement | 0.7 | YES | Nova drafts 1 paragraph |
