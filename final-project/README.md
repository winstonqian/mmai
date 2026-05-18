# Final Project: NeuroCLIP + LATA

**Action Semantics and Latency-Aware Alignment for EEG-to-Video Decoding**  
Winston Qian · Rachel Li · Emma Wang  
MIT Multimodal AI, Spring 2026

This project studies EEG-to-video decoding on SEED-DV through two diagnostic
questions:

1. **Which visual concepts are actually decodable from EEG?**
2. **When does the neural evidence for a video event arrive relative to the
   stimulus?**

Instead of treating aggregate 40-way accuracy as the whole story, we audit the
benchmark, analyze per-concept failure modes, and learn temporal response delay.

---

## Main Contributions

### 1. Baseline validity audit

We reproduced EEG2Video-style within-subject concept classification and audited
the setup for common EEG benchmark artifacts.

- Leave-one-block-out within-subject evaluation.
- Train-only normalization to avoid cross-split leakage.
- Run-position stratification across the five same-concept clips in each block.
- Within-concept prediction consistency against an empirical random baseline.

The audit found above-chance semantic signal without evidence of a simple
monotonic run-position shortcut.

### 2. NeuroCLIP: CLIP-aligned EEG concept retrieval

NeuroCLIP maps EEG features into a frozen CLIP concept space and evaluates
40-way concept retrieval. Its main value is interpretability: it lets us ask
which concepts are decodable and whether CLIP geometry explains success.

Key finding: **CLIP geometry does not explain EEG decodability.** Concepts that
are isolated in CLIP space are not systematically easier to decode from EEG.
Instead, activity-rich concepts such as sports, music, and people are much more
decodable than passive scenes.

### 3. LATA: Latency-Aware Temporal Alignment

LATA learns a soft distribution over candidate EEG-video delays during
contrastive chunk alignment. This tests whether temporal alignment should assume
zero lag or account for biological response latency.

Key finding: **all subjects prefer a nonzero neural delay.** On SEED-DV, 14/20
subjects peak at a two-chunk delay, 6/20 peak at a one-chunk delay, and no
subject peaks at zero lag.

---

## Key Results

| Result | Value |
|---|---:|
| Supervised DE baseline Top-1 | 4.37% ± 2.64% |
| Supervised DE baseline Top-5 | 17.17% ± 5.44% |
| NeuroCLIP text+image Recall@1 | **4.60% ± 2.70%** |
| NeuroCLIP text+image Recall@5 | **17.47% ± 5.14%** |
| Chance Recall@1 / Recall@5 | 2.50% / 12.50% |
| Activity-rich concept Recall@1 | **6.79%** |
| Passive concept Recall@1 | 3.83% |
| Activity vs. passive test | t = 6.72, p = 5.95e-8 |
| CLIP isolation vs. EEG Recall@1 | r = 0.036, p = 0.827 |
| LATA peak delay counts | 14/20 at δ=2, 6/20 at δ=1 |
| LATA expected delay | 1.58 ± 0.05 chunks ≈ 790 ms |

---

## Repository Structure

```text
final-project/
├── README.md
├── motivation.png
├── final_report/
│   ├── final_report.tex
│   ├── references.bib
│   ├── neurips_2025.sty
│   └── figures/
│       ├── neuroclip_summary.png
│       ├── concept_decodability.png
│       ├── category_r1_analysis.png
│       ├── lata_synthetic_validation.png
│       └── lata_all_subjects_results.png
└── EEG2Video/
    ├── neuroclip/
    │   ├── train_neuroclip.py
    │   ├── models_neuroclip.py
    │   ├── dataset.py
    │   ├── concept_decodability.py
    │   ├── category_r1_analysis.py
    │   ├── frequency_band_profile.py
    │   └── ... additional analysis scripts
    ├── lata/
    │   ├── lata.py
    │   ├── synthetic_validation.py
    │   ├── train_lata_seeddv.py
    │   ├── train_all_subjects.py
    │   └── plot_seeddv_results.py
    └── analysis/
        ├── analyze_all.py
        ├── generate_summary_tables.py
        └── summary_tables.md
```

---

## Final Report

The final report source is in [`final_report/`](./final_report/).

Primary files:

- [`final_report/final_report.tex`](./final_report/final_report.tex)
- [`final_report/references.bib`](./final_report/references.bib)
- [`final_report/figures/`](./final_report/figures/)

The report uses the NeurIPS format and is written as a conventional research
paper: abstract, introduction, related work, problem statement, method,
experiments, results, discussion, and conclusion/future work.

If compiling locally:

```bash
cd final_report
latexmk -pdf final_report.tex
```

If the overview motivation figure is enabled in the LaTeX source, include the
top-level [`motivation.png`](./motivation.png) when uploading to Overleaf.

---

## Takeaway

The project does not claim to solve EEG-to-video decoding. Instead, it sharpens
what the benchmark is telling us:

- EEG concept decoding on SEED-DV is weak in absolute accuracy but meaningfully
  above chance.
- Decodability is selective: activity-rich concepts are easier than passive
  concepts.
- CLIP semantic isolation is not what determines EEG decodability.
- EEG-video alignment should not assume synchronous video and neural streams.

Together, NeuroCLIP and LATA turn EEG-to-video decoding from a single accuracy
number into a semantic and temporal analysis problem.
