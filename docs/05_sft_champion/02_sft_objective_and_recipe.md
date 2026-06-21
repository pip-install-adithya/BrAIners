# SFT objective and training recipe

This file documents the supervised finetuning objective and the design choices behind the SFT champion.

## 1. Training objective

Let the prompt be $x$ and the target completion be $y = (y_1, y_2, \dots, y_T)$.

The standard SFT objective is the negative log-likelihood:

$$L_{\text{SFT}}(\theta) = -\sum_{t=1}^{T} \log \pi_\theta(y_t \mid x, y_{<t})$$

This is the base loss that teaches the model to follow the desired reasoning-and-answer format.

---

## 2. LoRA parameterization

Rather than updating every weight in the model, the SFT setup uses Low-Rank Adaptation (LoRA).

For a weight matrix $W_0$, LoRA parameterizes the update as:

$$W = W_0 + \Delta W = W_0 + BA$$

where:
- $W_0$ is frozen,
- $A$ and $B$ are the trainable low-rank adapters,
- The rank $r$ is kept small enough to preserve the pretrained geometric representation.

This is the right choice here because the project’s evidence suggests the model already has useful latent reasoning structure. It does not need a full parameter rewrite; it needs controlled steering.

---

## 3. Why SFT was preferred over heavier retraining

The mechanistic experiments showed that:
- The model is already structurally capable.
- The main bottleneck is late answer routing.
- The biggest performance gains come from better formatting, extraction stability, and prompt discipline.

That means SFT is a better first-stage intervention than full retraining. It is cheaper, more stable, and easier to preserve.

---

## 4. Reasoning format

The SFT data enforces a structured format with explicit reasoning and final answer separation:

$$\langle think \rangle \dots \langle /think \rangle \qquad \langle answer \rangle \dots \langle /answer \rangle$$

This structural tag enforcement matters because downstream evaluation depends heavily on extracting the final answer robustly. The project repeatedly found that answer-format discipline is a real source of score improvement, not a cosmetic detail.

---

## 5. Why this recipe works

The SFT recipe works because it aligns three core layers of the system:

1. **The training objective:** The model learns the preferred token layout and answer syntax.
2. **The evaluation pipeline:** The benchmark scorer can reliably parse the final response out of the target slot.
3. **The mechanistic reality:** The model already routes useful information late in the residual stream, so supervised format learning helps it finalize that answer track more cleanly.

---

## 6. What SFT is optimizing in practice

* **GSM8K:** The model learns to preserve the reasoning trace long enough to emit the final numerical value cleanly.
* **StrategyQA:** The model learns to compress multi-step uncertainty into a binary yes/no decision.
* **MMLU:** The model learns to select the correct choice option letter without collapsing into a brittle extraction artifact.

---

## 7. Summary

The SFT recipe is simple, but it is not shallow. It is grounded in the observed failure modes:
- Late answer commitment
- Format fragility
- Answer-slot bias
- Extraction sensitivity

That is why this checkpoint became the champion.