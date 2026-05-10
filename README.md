# MMAI 2026 — Winston Qian

Welcome to my course portfolio for **6.S985: Modeling Multimodal AI 2026** at MIT/Harvard.  
This repository is a living lab notebook: homework, experiments, and a final project that evolved from a baseline audit into a genuine research finding.

🌐 **[Live Site](https://winstonqian.github.io/mmai/)**

---

## Final Project — NeuroCLIP

**[NeuroCLIP: Action Semantics Governs EEG Concept Decodability](./final-project/)**  
*Winston Qian · Rachel Li · Emma Wang*

> In contrastive EEG-to-CLIP retrieval, concept decodability is not determined by CLIP embedding geometry — it is determined by **action semantic content**. Dynamic human activity concepts are decoded with ~80% higher accuracy than passive object scenes (6.8% vs. 3.8%, p < 10⁻⁷), consistently across all 7 recording sessions and all subjects. This is not a raw EEG amplitude effect — it is a dataset-agnostic principle for designing more decodable BCI stimulus sets.

### What we built
- **NeuroCLIP**: lightweight CNN encoder mapping 62-channel × 5-band DE features → 512-D CLIP-aligned embeddings, trained with 40-way contrastive loss against a frozen CLIP gallery (zero-shot at test time)
- **4.60% ± 2.70% Top-1 R@1** on 40-way concept retrieval — matching the supervised DE baseline (4.37%) without any concept labels at test time
- **47 analysis figures, 45 scripts** — frequency band ablation, brain region ablation, category centroid RSA, session × category interaction, subject scaling, optimal stimulus design, and more

### The story in 5 steps
1. **Baseline audit**: confirmed no run-position artifacts, no data-leak inflation, and 24.3% within-concept consistency vs. 17.8% random — genuine semantic signal
2. **Built NeuroCLIP**: zero-shot CLIP-aligned EEG retrieval, competitive with supervised baselines
3. **CLIP geometry null**: per-concept CLIP isolation → per-concept R@1: r = 0.036, p = 0.83 (not significant)
4. **Action semantics finding**: Activity concepts 6.8% vs. Passive 3.8% (p < 10⁻⁷, 7/7 sessions, not an amplitude effect)
5. **Design principle**: activity-selected top-10 concepts → 6.97% R@1 (+55% relative over all-40)

📁 [Code + all figures](./final-project/EEG2Video/neuroclip/)

---

## Homework

| # | Topic | Summary |
|---|-------|---------|
| [HW1](./homework/homework-1/) | Dataset | Multimodal TVQA Preprocessing — extracting visual, textual, and temporal modalities |
| [HW2](./homework/homework-2/) | Fusion | Multimodal Fusion & Alignment — early/late/tensor fusion + contrastive learning on TVQA |
| [HW3](./homework/homework-3/) | VLM | VLM Fine-Tuning — Qwen2.5-VL with LoRA for zero-shot action reasoning on TVQA |
| HW4 | TBD | — |
| HW5 | TBD | — |

---

## License
<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a>  
Licensed under [CC BY-SA 4.0](http://creativecommons.org/licenses/by-sa/4.0/).
