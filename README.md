# Project ReasonEdge

- **Problem Statement Number** - 06
- **Problem Statement Title** - *Enhancing Reasoning in Small Language Models (SLMs) using Reinforcement Learning*
- **Team name** - *BrAIners*
- **Team members (Names)** - *Adithya Lakshminarayanan*, *Thanish Vardhan B*
- **Institute/College Name** - *Indian Institute of Technology Madras*, *Adyar, Chennai*
- **Final Presentation Google Drive Link** - *[Drive PDF](https://drive.google.com/file/d/1cY8gm2o9fL3WnTpndghEQ0kpsM2F7Bac/view?usp=sharing)*
- **Full Submission Demo Video Link** - *[YT Demo Video](https://youtu.be/71GWrhE6G2Q)*
- **Setup & Result Reproducibility Video Link** - *[YT Setup Video](https://youtu.be/61bKzQ845JA)*

## Overview

ReasonEdge is an open-weight reasoning project built on top of **Phi-3-mini**.  
The repository contains:

- a strong **SFT champion** checkpoint,
- multiple **RL attempts** including GRPO, hierarchical steering GRPO, and RRPO/DPO-style hard-mining,
- extensive **mechanistic interpretability** work using TLens-style residual stream analysis,
- and full **benchmark evaluation** for GSM8K, StrategyQA, and MMLU.

The project was developed to study and improve the reasoning behavior of small language models through a combination of:
- supervised finetuning,
- calibrated evaluation,
- mechanistic analysis,
- and RL-based refinement.

---

## Project Artefacts

### Technical Documentation
The `docs/` folder contains detailed markdown documentation covering:
- project story and motivation,
- technical architecture,
- implementation details,
- installation instructions,
- user guide,
- salient features,
- SFT champion analysis,
- RL attempts,
- TLens / mechanistic interpretability reports,
- and a full `docs/ax.md` file describing the agentic development workflow and what worked / did not work.

### Source Code
The `src/` folder contains all major code and experiment artifacts, including:
- benchmark evaluation notebooks and scripts,
- SFT training code,
- GRPO / hierarchical steering / RRPO-DPO training code,
- TLens and residual-stream analysis notebooks,
- experiment outputs,
- CSV summaries,
- plots,
- and saved adapters / checkpoints.

### Models Used
- `microsoft/phi-3-mini-4k-instruct` — Hugging Face: https://huggingface.co/microsoft/phi-3-mini-4k-instruct

### Models Published
- *Nothing has been published to Hugging Face.*

### Datasets Used
- GSM8K — https://huggingface.co/datasets/openai/gsm8k
- StrategyQA — https://huggingface.co/datasets/ChilleD/StrategyQA
- MMLU — https://huggingface.co/datasets/cais/mmlu

### Datasets Published
- *Nothing has been published to Hugging Face.*

---

## Repository Structure

### `docs/`
Documentation for the entire project.

Important folders include:
- `docs/01_project_story/` — project story, problem framing, and overall motivation
- `docs/02_initial_six_experiments/` — the first six diagnostic experiments
- `docs/03_advanced_five_experiments/` — the five deeper mechanistic experiments
- `docs/04_tlens/` — residual-stream / TLens reports
- `docs/05_sft_champion/` — complete SFT documentation
- `docs/06_rl_attempts/` — GRPO, hierarchical steering, and RRPO/DPO attempts
- `docs/ax.md` — agentic AI and development workflow write-up
- `docs/overview.md` — high-level documentation overview

### `src/`
All experiment and training code, including:
- baseline benchmarking,
- SFT training,
- RL training attempts,
- TLens experiments,
- and saved outputs / figures / checkpoints.

Key subfolders include:
- `src/experiments/`
- `src/advanced_experiments/`
- `src/t_lens/`
- `src/phi3_adapters/`
- `src/final_best_code/`
- `src/file_dump/`

---

## Technical Documentation Summary

The documentation explains:
- how the Phi-3-mini backbone was used,
- how SFT was trained,
- how benchmark evaluation was done,
- why the benchmark pipeline had to be fixed carefully,
- why the TLens work mattered,
- why the SFT checkpoint became the champion,
- and how the RL attempts evolved from generic GRPO to hierarchical steering and finally RRPO/DPO-style hard mining.

---

## Final Presentation

The final presentation covers:
- the project motivation,
- the model and dataset setup,
- the benchmark results,
- the mechanistic interpretability findings,
- the RL exploration path,
- the final SFT champion.

---

## Demo Video

The demo video shows the end-to-end solution in action, including:
- interactive inference,
- reasoning-style outputs,
- and the final answer generation pipeline.

---

## Setup & Reproducibility Video

The reproducibility video shows:
- environment setup,
- dataset/model download steps,
- training execution,
- evaluation execution,
- and reproduction of the experiments.

---

## Attribution

This project is built on top of public open-weight models, public benchmark datasets, and open-source tooling.

Original project and tooling references are listed in the documentation section where appropriate, along with the new features developed for ReasonEdge.

---

## Project Summary

ReasonEdge is designed to show that the biggest improvements in small language models come from:
- better supervised finetuning,
- better evaluation,
- better mechanistic understanding,
- and more targeted refinement than generic RL alone.

The strongest stable checkpoint is the plain SFT model, while the RL attempts serve as a structured exploration of what still remains to be improved.