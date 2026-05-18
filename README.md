# MMAI 2026 — Winston Qian

Welcome to my course portfolio for **6.S985: Modeling Multimodal AI 2026** at MIT/Harvard.  
This repository is a living lab notebook: homework, experiments, and a final project that evolved from a baseline audit into a genuine research finding.

🌐 **[Live Site](https://winstonqian.github.io/mmai/)**

---

## Final Project — NeuroCLIP + LATA

**[Action Semantics and Latency-Aware Alignment for EEG-to-Video Decoding](./final-project/)**  
*Winston Qian · Rachel Li · Emma Wang*

> EEG-to-video decoding should not be evaluated only by aggregate accuracy. On
> SEED-DV, we show that concept decodability is **semantic** and **delayed**:
> activity-rich concepts are much easier to decode than passive scenes, while
> learned EEG-video alignment consistently avoids zero lag.

### What we built
- **Baseline audit**: reproduced EEG2Video-style within-subject concept
  classification and checked normalization leakage, run-position shortcuts, and
  within-concept consistency.
- **NeuroCLIP**: CLIP-aligned EEG concept retrieval probe for asking which
  SEED-DV concepts are decodable and why.
- **LATA**: latency-aware temporal alignment module that learns a soft
  distribution over EEG-video delay during contrastive chunk training.

### Key results
- **NeuroCLIP Recall@1**: 4.60% ± 2.70%, comparable to the supervised DE
  baseline at 4.37% ± 2.64%.
- **CLIP geometry null**: per-concept CLIP isolation does not predict EEG
  decodability (r = 0.036, p = 0.827).
- **Action semantics finding**: activity-rich concepts decode better than
  passive concepts (6.79% vs. 3.83%, t = 6.72, p = 5.95e-8).
- **Latency finding**: LATA learns nonzero delay for every subject; 14/20 peak
  at δ=2, 6/20 peak at δ=1, and none peak at zero lag.
- **Expected delay**: 1.58 ± 0.05 chunks, approximately 790 ms.

📁 [Final project overview](./final-project/)  
📄 [Final report source](./final-project/final_report/)  
🧠 [EEG2Video / NeuroCLIP / LATA code](./final-project/EEG2Video/)

---

## Homework

| # | Topic | Summary |
|---|-------|---------|
| [HW1](./homework/homework-1/) | Dataset | Multimodal TVQA Preprocessing — extracting visual, textual, and temporal modalities |
| [HW2](./homework/homework-2/) | Fusion | Multimodal Fusion & Alignment — early/late/tensor fusion + contrastive learning on TVQA |
| [HW3](./homework/homework-3/) | VLM | VLM Fine-Tuning — Qwen2.5-VL with LoRA for zero-shot action reasoning on TVQA |
| [HW4](./homework/homework-4/) | RLHF / GRPO | Reinforcement Learning for VLMs — GRPO + LoRA on TVQA with accuracy and format rewards |
| [HW5](./homework/homework-5/) | Agents | AI Agents in the Wild — ReAct-style Wikipedia research agent with custom tools and evaluation |

---

## License
<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a>  
Licensed under [CC BY-SA 4.0](http://creativecommons.org/licenses/by-sa/4.0/).
