# PermaFrost — Revision Roadmap (new framing)

Status legend: `[ ]` todo · `[~]` in progress · `[x]` done

## 0. Core reframing (decide first — everything depends on it)

**New thesis:** *We introduce a geometric forensic framework — Thermodynamic Length and the Infection Traceback Graph (ITG) — that detects and localizes latent, triggerable backdoors from a model's internal computation, invisible to output-only evaluation. We motivate it with Stealth Pretraining Seeding (SPS), a threat model, and validate it under a controlled SFT proxy and a continual-pretraining setting.*

- [ ] Primary contribution = the **diagnostics framework** (what all reviewers praised).
- [ ] SPS = **motivating threat model**, not a novelty claim (stop competing with Carlini/Souly/Chen on "new attack").
- [ ] Fixed vocabulary everywhere: **SPS** = threat model · **PermaFrost** = conceptual attack · **PermaFrost-Attack** = controlled instantiation.

> Note: reframing is necessary but not sufficient. The blocker is **soundness** (2 / 2 / 2.5 / 3.5). The Tier-1/2 experiments below are what lift it.

## 1. Section-by-section rewrite

- [ ] **Title/abstract:** lead with the diagnostic framework; fix "planting" → "Planting"; state the 3-term vocabulary once.
- [ ] **Introduction:** reorder contributions — (1) framework, (2) SPS motivation, (3) empirical signatures; scope down web-scale language to motivation, not demonstration.
- [ ] **Threat model (§2):** shorten; position SPS vs Carlini (2024) and Souly et al. (2025); state weaker-capability distinction; label SFT as a proxy up front.
- [ ] **Methods (§3):** expand derivations (L236–243), define symbols at L236/L243, make ITG gradient notation explicit ($g_v=\nabla_{a_v}z_{\text{target}}\in\mathbb{R}^d$), unify logit-lens vs tuned-lens usage + citation.
- [ ] **Experiments (§4):** reorganize around the framework's *detection* value, not attack success.
- [ ] **Related work:** add positioning vs geometric-alignment line (Arditi, Pan, Wollschläger) and backdoor-forensics line (CROW, BAHA).
- [ ] **Conclusion:** rewrite to match the abstract (claim the framework; don't redefine PermaFrost).

## 2. Experiments

### Tier 1 — soundness-critical (do first)
- [~] **Continual-pretraining result** (answers all 4 reviewers). Checkpoint trained; run geometric analysis.
  - [ ] **LINCHPIN CHECK:** does the CPT model actually *refuse clean prompts*? If yes → headline C1 / decision-valley result. If no → reframe as signature-emergence / dose–response, do not claim a clean-refusal valley.
- [ ] **Interventional ITG validation** (2Z6U; paper's own "future work"). Pathway ablation vs random-layer controls + activation patching. Code already exists in the eval notebook (`run_itg_validation`) — run it and collect numbers.

### Tier 2 — baseline gaps (all reviewers)
- [ ] **CROW** internal-consistency metric on our models — also resolves the "sharper vs smoother" tension with data.
- [ ] **BAHA** attention-head attribution comparison.
- [ ] **BackdoorLLM** positioning (attack setup + geometric signatures).

### Tier 3 — quantitative rigor (cheap, high payoff)
- [~] **Decision-valley-depth** stats with 95% CIs (clean vs triggered + gap). Use `PermaFrost_Analysis.ipynb` on saved `metrics.npz`.
- [ ] **Distance-metric ablation** (Fisher–Rao vs KL / Euclidean / cosine) — requires recomputing trajectories from the model (GPU).
- [ ] **Full-FT vs QLoRA** side-by-side to kill the "LoRA artifact" concern.

## 3. Writing / presentation fixes (batch, cheap)
- [ ] Vectorize Figure 4 (PDF/SVG) + de-crowd prompt axis.
- [ ] Fix missing paren at L1586.
- [ ] Correct Skean et al. citation (L229–232 / L265–268).
- [ ] Unify lens terminology + citation.
- [ ] **Remove author info from Page-1 code listing; notify AC (anonymity — desk-issue risk).**

## 4. Sequencing
- **Phase 1 (now → rebuttal deadline):** lock reframing; run CPT analysis + ITG ablation; do all cheap writing/anonymity fixes. Goal: ≥1 Tier-1 result in hand.
- **Phase 2 (rebuttal → resubmission):** finish Tier-2 baselines + Tier-3 stats; rewrite abstract/intro/conclusion; figure overhaul.
- **Phase 3 (polish):** related-work positioning; terminology consistency pass; verify every rebuttal promise is delivered in the manuscript.

## 5. Open decisions
- [ ] Does the CPT SmolLM refuse clean prompts? (determines headline vs supporting result)
- [ ] Target current-cycle rebuttal or resubmission? (determines how much of Tier 1–2 must be *done* vs *promised*)
