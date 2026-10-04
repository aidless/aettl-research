# Multi-Modal Emergent Policy Contagion (MM-EPC) — SUPERSEDED SNAPSHOT

> ⚠️ **已归档快照（2026-10-03 标注）**：本仓库是本项目的**早期版本**，最终版在
> **[github.com/aidless/mm-epc](https://github.com/aidless/mm-epc)**，以该仓 README 的结论为准。
>
> **关键差异**：本快照的核心头条（方向不对称显著，p = 0.008）在最终版分析中**未获支持**——
> 加入更多条件与预注册协议后，方向不对称不再显著；由此催生的"结论对评估条件敏感"问题
> 单独发展成了 N-Sensitivity 诊断研究（paper4）。本仓保留作为第一轮证据与溯源。
>
> 另注：本快照内部数字本就不一致（TL;DR 引 γ 0.869/0.851，下表为 0.847/0.832）——
> 两套数字均被最终版取代，请勿引用。

**Asymmetric Strategy Transfer Between Text and Visual Reasoning** — a research project on how reasoning strategies leak across AI model modalities.

> **TL;DR (initial round, superseded)**: The initial round found that when AI models are trained on text tasks with visual strategies (or vice versa), strategy transfer appeared *asymmetric* — visual-to-text contamination seemingly stronger than text-to-visual (p = 0.008). **The final version did not confirm this significance**; see [mm-epc](https://github.com/aidless/mm-epc) for the corrected claims.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://www.python.org/)

---

## Why This Project Matters

This is a **research paper** investigating a fundamental question in multi-modal AI: when a model is trained on both text and visual reasoning tasks, do the reasoning strategies *contaminate* each other — and if so, which direction is stronger?

The answer matters for anyone building multi-modal AI systems (GPT-4V, Gemini, Claude Opus 4 with vision): **your evaluator and training conditions may silently shape your measured conclusions.**

**Initial-round result** (superseded): Visual-to-text strategy transfer (γ_V→T) appeared significantly stronger than text-to-visual (γ_T→V), p = 0.008. The final preregistered analysis found this asymmetry not significant.

---

## What We Found (initial round — numbers as recorded in this snapshot)

### 1. Strategy Contagion Exists

Reasoning strategies *emerge* and *propagate* across modalities. This isn't just "the model gets better at both" — it's "the model silently adopts strategies from one modality while working in another."

| Phase | Metric | Result | Significance |
|-------|--------|--------|-------------|
| **1: PCI** | Cross-modal Policy Contagion Index | **1.464** | 3.2× stronger than text-only |
| **2: Asymmetry** | γ_V→T vs γ_T→V | **0.847** vs 0.832 | p = 0.008 (not replicated in final version) |
| **3: Significance** | Bootstrap validation | CI: [0.001, 0.029] | p = 0.004 (not replicated in final version) |

### 2. Key Findings (Plain English — initial round)

1. **Visual strategies appeared to "infect" text reasoning more strongly** — not confirmed at significance in the final version
2. **Strategy reversal after cross-contamination** — pure-text models use "synthesis" strategy; after visual training, they switch to "step-by-step"; visual models do the opposite
3. **Visual strategies are under-utilized** — visual strategies account for only 9.1% of optimal weights, suggesting current multi-modal training is suboptimal

### 3. Implications for Engineering

| Implication | What It Means |
|-------------|---------------|
| **Evaluation conditions dominate** | The same pipeline can produce p = 0.008 or p ≈ 0.5 depending on conditions — measure N-sensitivity before trusting any headline number |
| **Multi-modal architecture** | Don't let visual strategies silently contaminate text reasoning without measurement |
| **Safety** | Contagion patterns could enable adversarial attacks — an attacker might poison visual data to degrade text performance |
| **Evaluation** | Don't just measure overall accuracy — measure cross-modal strategy transfer directly |

---

## Reproducing the Results

### Installation
```bash
pip install numpy scipy matplotlib
```

### Run the Full Pipeline
```bash
# Phase 1: Compute Policy Contagion Index
python mm_epc_phase1.py

# Phase 2: Measure asymmetric transfer (γ_V→T vs γ_T→V)
python mm_epc_phase2_contagion.py

# Phase 3: Bootstrap significance validation
python mm_epc_phase3_significance.py
```

**Note**: 脚本需要环境变量或 .env 提供 API key（历史版本曾硬编码，key 已吊销并从当前版本移除）。

### Expected Output (initial round)
```
Phase 1: PCI = 1.464 (3.2x stronger than text-only baseline)
Phase 2: γ_V→T = 0.869, γ_T→V = 0.851, p = 0.008
Phase 3: 95% CI [0.001, 0.029], one-sided p = 0.004, Cohen's d = 0.89
```

---

## Repository Structure

```
mm-epc/
├── README.md                    ← you are here
├── paper/
│   ├── mm_epc_paper.tex       ← LaTeX source (NeurIPS 2026 format)
│   ├── mm_epc_paper.bib       ← bibliography
│   └── arxiv_submission_guide.md
├── experiments/
│   ├── phase1_pci.json         ← Phase 1 raw results
│   ├── phase2_contagion.json  ← Phase 2 raw results
│   └── phase3_significance.json
├── code/
│   ├── mm_epc_phase3_significance.py  ← statistical validation
│   └── visualization.py            ← paper figures
├── figures/
│   ├── fig1_strategy_weights.pdf
│   ├── fig2_pci_comparison.pdf
│   ├── fig3_contagion_heatmap.pdf
│   ├── fig4_strategy_shift.pdf
│   └── fig5_modality_breakdown.pdf
└── requirements.txt
```

---

## Paper

- **Title**: Multi-Modal Emergent Policy Contagion: Asymmetric Strategy Transfer Between Text and Visual Reasoning
- **Status**: superseded snapshot — final version at [mm-epc](https://github.com/aidless/mm-epc) (in submission)
- **PDF**: [`paper/mm_epc_paper.pdf`](paper/mm_epc_paper.pdf)

---

## Citation

本快照不再建议引用。请引用最终版（见 [mm-epc](https://github.com/aidless/mm-epc) README 的 Citation 区）。

---

## For Recruiters

This project demonstrates:

1. **Research ability** — formulated a novel hypothesis, designed experiments, collected results, drew conclusions
2. **Python engineering** — clean experiment code, reproducible pipeline, statistical validation
3. **AI/ML knowledge** — understanding of multi-modal models, reasoning strategies, cross-modal transfer
4. **Academic communication** — paper writing, visualization, statistical rigor
5. **Research integrity** — 自己的头条结论被自己的最终版推翻时，公开标注、给出修正，并把它变成新的方法论（N-Sensitivity）

**I'm open to AI Application Developer / AI Researcher roles.**  
GitHub: [@aidless](https://github.com/aidless)

---

*Liu Zewen (刘泽文) — B.Eng. Software Engineering 2026, Qilu Institute of Technology*
