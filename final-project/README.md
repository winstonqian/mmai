# Final Project — NeuroCLIP

**NeuroCLIP: Action Semantics Governs EEG Concept Decodability**  
Winston Qian · Rachel Li · Emma Wang · MIT Spring 2026

→ All code, figures, and results live in [`EEG2Video/neuroclip/`](./EEG2Video/neuroclip/)

---

## What This Is

NeuroCLIP is a zero-shot EEG-to-video retrieval system. Given a brain signal recorded while someone watches a video, it retrieves the correct video concept from a 40-item library — without any concept labels at test time. It works by aligning EEG representations to frozen CLIP embeddings via contrastive learning.

**The bigger finding:** concept decodability is not explained by CLIP geometry. It is explained by action semantic content. Concepts depicting dynamic human activity decode ~80% better than passive object scenes.

---

## Key Results

| | |
|---|---|
| Top-1 R@1 (NeuroCLIP, zero-shot) | **4.60% ± 2.70%** |
| DE supervised baseline | 4.37% ± 2.64% |
| Chance | 2.50% |
| Activity concepts R@1 | **6.8%** |
| Passive concepts R@1 | **3.8%** |
| Significance | t=6.72, p < 10⁻⁷ |
| Sessions where Activity > Passive | **7 / 7** |
| Top-10 activity-selected subset | **6.97%** (+55% vs. all-40) |

---

## Repository Structure

```
EEG2Video/
├── neuroclip/
│   ├── train_neuroclip.py          # Main training script
│   ├── models_neuroclip.py         # CNN encoder architecture
│   ├── dataset.py                  # SEED-DV data loading
│   ├── category_r1_analysis.py     # Core finding: activity vs. passive
│   ├── session_category_interaction.py  # 7/7 session robustness
│   ├── frequency_band_profile.py   # Raw amplitude null result
│   ├── category_centroid_analysis.py    # RSA: ρ=0.645***
│   ├── concept_decodability.py     # CLIP isolation null
│   ├── ... (45 scripts total)
│   ├── figures/                    # 47 analysis figures
│   └── results/                    # JSON results (checkpoints excluded)
└── analysis/                       # Baseline audit results (Phase 1)
```

---

## The Research Story

**Phase 1 — Baseline Audit:** We audited the SEED-DV baseline for protocol artifacts before building anything. Run-position profiles were flat (no anticipation shortcut). Data-leak correction didn't inflate mean accuracy. Within-concept prediction consistency was 24.3% vs. 17.8% random — genuine semantic signal. The baseline is clean.

**Final project:** We built NeuroCLIP (zero-shot CLIP alignment), then asked: *why do some concepts decode better than others?* The obvious answer — CLIP geometry — turned out to be wrong (r=0.036, p=0.83, null). The actual driver is action semantic content: concepts involving dynamic human activity (sports, music, people) decode with ~80% higher R@1 than passive scenes, across all sessions and subjects, and the effect is not explained by raw EEG amplitude differences.

The practical implication: selecting 10 activity-rich concepts instead of all 40 yields +55% relative improvement in retrieval accuracy — a dataset-agnostic design principle for EEG-BCI stimulus sets.
