# Technical Documentation

## 1. Project Overview

This project investigates how to improve reasoning in small language models using a combination of supervised finetuning, mechanistic interpretability, and reinforcement-learning-style refinement. The final system is built around an open-weight backbone model and is evaluated on GSM8K, StrategyQA, and MMLU.

The project is structured around three main goals:

1. Build a strong and stable supervised baseline.
2. Diagnose failure modes using interpretability and benchmark analysis.
3. Explore targeted RL-style refinement methods that focus on the model’s remaining weaknesses.

---

## 2. Technical Stack

### Core model stack
- Backbone model: `microsoft/phi-3-mini-4k-instruct` - [HF Page](https://huggingface.co/microsoft/Phi-3-mini-4k-instruct)
- Parameter-efficient finetuning: LoRA / PEFT
- Quantization support: bitsandbytes 4-bit loading
- Inference and training: PyTorch + Hugging Face Transformers

### Evaluation and benchmarking
- GSM8K evaluation
- StrategyQA evaluation
- MMLU evaluation
- Random sampled held-out subsets
- Exact-match and task-specific parsing

### Interpretability / analysis
- Residual-stream analysis
- Token-probability tracking
- Layerwise dashboard plots
- Attention and logit-lens style inspection
- Sequence-dynamics visualizations

### Visualization and reporting
- Matplotlib
- Pandas
- NumPy
- JSON / CSV artifact export
- Markdown documentation

### Execution environment
- Kaggle notebook environment
- CUDA-enabled GPUs
- Optional 4-bit loading for memory safety
- Reproducible random seeds

---

## 3. Open-Source Libraries and Projects Used

### Core libraries
- PyTorch
- Transformers
- Datasets
- PEFT
- bitsandbytes
- NumPy
- Pandas
- Matplotlib

### Benchmark datasets
- GSM8K
- StrategyQA
- MMLU

### Related open projects and tooling
- Hugging Face Transformers ecosystem
- PEFT / LoRA ecosystem
- TRL-style policy optimization concepts
- Mechanistic interpretability tooling inspired by residual-stream analysis workflows

---

## 4. Technical Architecture

The solution is organized into a modular pipeline.

### 4.1 Data layer
The data layer loads benchmark examples, samples held-out subsets, and prepares task-specific training and evaluation pools.

For each task:
- GSM8K uses math word problems with final numeric answers.
- StrategyQA uses binary yes/no questions.
- MMLU uses multiple-choice questions with A/B/C/D answers.

### 4.2 Prompting layer
Each task uses a task-specific prompt format:
- GSM8K: step-by-step reasoning plus final numeric answer
- StrategyQA: short reasoning plus yes/no answer
- MMLU: short reasoning plus single-letter answer

The prompting layer is important because the model is highly sensitive to output format and answer routing.

### 4.3 Model layer
The model layer consists of:
- a Phi-3-mini backbone,
- an SFT LoRA adapter,
- optional RL-style challenger checkpoints,
- and evaluation-time decoding logic.

### 4.4 Evaluation layer
The evaluation layer:
- generates answers,
- extracts final responses,
- checks correctness,
- saves prediction CSVs,
- and compares checkpoints.

### 4.5 Interpretability layer
The interpretability layer saves:
- residual norm plots,
- cosine-to-final-layer curves,
- token-probability heatmaps,
- and TLens-style dashboards.

### 4.6 Reporting layer
The reporting layer exports:
- CSV results,
- JSON summaries,
- figures,
- and markdown documentation.

---

## 5. Implementation Details

### 5.1 SFT training
The SFT stage trains the model using supervised next-token prediction on benchmark-style examples.

The objective is:

$$
L_{\text{SFT}}(\theta) = -\sum_{t=1}^{T} \log \pi_\theta(y_t \mid x, y_{<t})
$$

where:
- $x$ is the input prompt,
- $y$ is the target completion,
- $\pi_\theta$ is the model distribution.

### 5.2 LoRA adaptation
Instead of updating the full backbone, the training uses LoRA:

$$
W = W_0 + BA
$$

where:
- $W_0$ is the frozen base weight,
- $A$ and $B$ are trainable low-rank matrices.

This keeps training efficient and stable.

### 5.3 RL-style refinement
The later refinement stages use reward shaping, preference optimization, and hard-example mining.

A generic RL objective can be written as:

$$
J(\theta) = \mathbb{E}_{y \sim \pi_\theta(\cdot \mid x)} [R(x,y)]
$$

where $R(x,y)$ measures correctness, format quality, and answer routing.

### 5.4 Hard-example mining
Examples that repeatedly fail are given higher weight:

$$
w_i = 1 + \lambda h_i
$$

where $h_i$ is a hardness score.

### 5.5 Preference optimization
A DPO-style objective compares a better completion $y^+$ and worse completion $y^-$:

$$
L_{\text{DPO}}(\theta)
=
-\log \sigma \left(
\beta \left[
\log \pi_\theta(y^+ \mid x) - \log \pi_\theta(y^- \mid x)
-
\log \pi_{\text{ref}}(y^+ \mid x) + \log \pi_{\text{ref}}(y^- \mid x)
\right]
\right)
$$

### 5.6 Residual-stream analysis
The interpretability pipeline tracks:
- residual norms,
- cosine similarity to the final layer,
- target-token probabilities over layers,
- and final-token confidence behavior.

This is used to understand how the model moves from internal reasoning to final answer emission.

---

## 6. Installation Instructions

Follow the instruction given in the [YT video](https://youtu.be/61bKzQ845JA).