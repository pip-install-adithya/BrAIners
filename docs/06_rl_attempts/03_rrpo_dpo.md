# RRPO / DPO-style hard-mining challenger

This file documents the final RL-style challenger developed for the project.

The key idea behind this stage is that the model does **not** need another generic reward loop.
It needs a more precise refinement process that focuses on the examples and answer routes that are still failing after SFT, calibration fixes, and the mechanistic interventions.

This is the final RL-style attempt because it is the most aligned with everything learned earlier:
- The TLens work showed that the bottleneck is late answer routing.
- The advanced experiments showed that calibration, permutation sensitivity, and self-correction are all conditional rather than universal.
- The benchmark logs showed that the remaining failures are concentrated in hard examples rather than distributed uniformly.

So this model is not a “bigger GRPO.” It is a targeted hard-mining and preference-optimization system.

---

## 1. Why this method was introduced

The project went through several phases:

### Phase 1: Baseline Reasoning
The baseline model already had useful latent structure, but it was unstable in the final answer stage.

### Phase 2: Supervised Finetuning
SFT improved the model substantially. It made the answer route cleaner and more stable.

### Phase 3: Generic GRPO
The first RL attempts were stable, but they did not reliably beat SFT. That told us the reward signal was too coarse.

### Phase 4: Hierarchical Steering
The hierarchical RL idea improved structure, but still did not clearly surpass the champion checkpoint.

### Phase 5: Hard-Mining RRPO / DPO
This final stage was introduced because the remaining failures were concentrated in a small number of informative cases. This means the training objective should not treat every example equally.

If we denote the policy as $\pi_\theta$, the prompt as $x$, and a completion as $y$, then a generic RL objective is:

$$J(\theta) = \mathbb{E}_{y \sim \pi_\theta(\cdot \mid x)}[R(x,y)],$$

where a plain reward $R(x,y)$ is simply not enough. The model’s failures are not only about correctness. They are multi-dimensional constraints mapping to:

$$\text{correctness} + \text{format} + \text{calibration} + \text{late routing} + \text{task-specific invariance}.$$

That is why the final challenger uses a structured objective instead of a single flat reward.

---

## 2. Why hard-example mining is central

The benchmark results showed that some examples are persistently hard across methods. This means the useful signal is not spread evenly across the dataset—some samples are significantly more informative than others.

Let each example $x_i$ have a hardness score $h_i$. Then a natural training weight is:

$$w_i = 1 + \lambda h_i,$$

where $\lambda > 0$ controls how strongly difficult examples are emphasized. The hard-mining loss can be written as:

$$L_{\text{hard}} = \sum_i w_i L(x_i).$$

This implementation ensures the project is not trying to memorize the entire dataset again, but is instead specifically repairing the model’s remaining weak spots.

### Why this is justified by the experiments
The earlier results showed that:
- Some GSM8K questions are solved cleanly while others collapse late.
- Some StrategyQA items have a strong latent signal but weak commitment.
- MMLU is often affected by answer-slot bias rather than pure knowledge failure.

Therefore, the remaining useful training signal is heavily concentrated in these hard cases, making hard mining the most direct way to exploit that distribution.

---

## 3. Why DPO-style preference optimization was added

The model does not only need to learn from static labels; it also needs to learn to prefer one completion path over another. This matters because many failures are not binary "right/wrong" errors, but rather relative quality drops:
- One completion is cleaner than another.
- One route is more decisive than another.
- One answer format is more benchmark-compatible than another.

Suppose for a prompt $x$ we have a better completion $y^+$ and a worse completion $y^-$. A standard DPO-style objective is formulated as:

$$L_{\text{DPO}}(\theta) = -\log \sigma \left( \beta \left[ \log \pi_\theta(y^+ \mid x) - \log \pi_\theta(y^- \mid x) - \log \pi_{\text{ref}}(y^+ \mid x) + \log \pi_{\text{ref}}(y^- \mid x) \right] \right),$$

where $\beta$ controls the sharpness of the preference update.

### Why this is useful here
Preference optimization is a strong fit because the project’s hard failures often follow clear patterns:
- The model possesses the requisite latent information but outputs it poorly.
- The model extracts the correct answer inside its hidden states but misses the final token route.
- The model produces a plausible completion, but fails to yield a benchmark-readable string.

This relative ranking task is exactly what preference learning handles better than a single sparse reward.

---

## 4. Why this is better than generic GRPO

The difference between the earlier GRPO family and this final method is a fundamental shift in training philosophy rather than just an implementation detail.

### GRPO asks:
> Which rollout is better right now?

### RRPO / DPO hard-mining asks:
> Which examples are still exposing the model’s weaknesses, and how do we directly train on those weaknesses?

Generic GRPO can move the policy, but it can also easily drift in the wrong direction if the reward proxy decouples from core capabilities. In contrast, the final challenger relies on:
- Hard-example selection
- Pairwise preference learning
- Routing-aware shaping
- Conservative, clipped policy refinement

---

## 5. Routing-aware regularization

The TLens mechanistic interpretability work directly inspired this layerwise regularizer. The residual-stream plots consistently showed that the model builds latent evidence early and finalizes the answer late. That means the final loss function cannot simply evaluate the terminal answer string; it must constrain the structural *route* into the answer.

Let $p_l$ be the probability of the target answer token at layer $l$, and let $\tau_l$ be a target curve that stays low early and rises late. The routing loss is written as:

$$L_{\text{route}} = \sum_{l \in \mathcal{L}} (p_l - \tau_l)^2 + \gamma \sum_{l} \max(0, p_l - p_{l+1}),$$

where:
- The first term encourages the answer token to follow the intended late-rise profile.
- The second term penalizes early collapse and non-monotonic routing behaviors ($\gamma$ acts as the penalty weight).

This provides a direct mathematical constraint reflecting our TLens dashboard observations: the answer route must remain latent early, grow sharply in the later layers, and stabilize near the end of the transformer stack.

---

## 6. Reward shaping for the benchmark tasks

The evaluation suites are not interchangeable, so the target reward formulation must reflect their distinct structural profiles.

### GSM8K
GSM8K is primarily a numeric reasoning and multi-step answer consolidation problem. A completion is useful if it reaches the correct numerical value, preserves a logical reasoning trace, and emits the final number cleanly. 

The task reward combines exact match accuracy, formatting, and a small length penalty to prevent rambling:

$$R_{\text{gsm8k}} = R_{\text{exact}} + \alpha R_{\text{format}} - \eta R_{\text{length}}.$$

### StrategyQA
StrategyQA is fundamentally a commitment and calibration problem. A correct answer is insufficient if the model does not actually commit cleanly. 

The reward explicitly weights target answer tokens and confidence:

$$R_{\text{stratqa}} = R_{\text{exact}} + \alpha R_{\text{format}} + \delta R_{\text{commitment}}.$$

### MMLU
MMLU is heavily sensitive to option-order permutations. The reward must protect against positional biases while enforcing syntax:

$$R_{\text{mmlu}} = R_{\text{exact}} + \alpha R_{\text{format}} + \rho R_{\text{invariance}}.$$

The project’s earlier permutation experiments showed that answer order can heavily distort the model’s apparent behavior, making the invariance term $\rho R_{\text{invariance}}$ vital.

---

## 7. Why the final objective is a mixture of terms

The complete RRPO-style objective is configured as a multi-task regularization loss:

$$L_{\text{RRPO}} = L_{\text{SFT}} + \lambda_{\text{DPO}} L_{\text{DPO}} + \lambda_{\text{route}} L_{\text{route}} + \lambda_{\text{hard}} L_{\text{hard}} + \lambda_{\text{fmt}} L_{\text{fmt}}.$$

Each component targets a specific failure mode:
- $L_{\text{SFT}}$: Keeps the model grounded in the target format and basic task behavior.
- $L_{\text{DPO}}$: Teaches the model to prefer cleaner, higher-quality completions.
- $L_{\text{route}}$: Forces the answer token to emerge in the correct late-layer pattern.
- $L_{\text{hard}}$: Focuses optimization power on the examples that still break the model.
- $L_{\text{fmt}}$: Guarantees benchmark-readable output syntax.

---

## 8. Why the method is staged

The training pipeline is intentionally executed in distinct stages to preserve weights stability:

1. **Warmup & Grounding**
2. **Preference Alignment**
3. **Online Clipped Refinement**
4. **Hard-Example Weight Scaling**
5. **Final Benchmark Evaluation**

Staging prevents catastrophic collapse. The earlier experiments showed that while the model possesses latent competence, the final answer stage remains fragile. Optimizing too early or too brutally causes the policy to game the reward proxy without improving actual capability.

---

## 9. Why the online refinement is clipped

The policy update is strictly bounded to prevent the model from drifting too far from its initialization point during online rollouts.

If we look at the importance ratio:

$$r_t(r) = \frac{\pi_\theta(y_t \mid x)}{\pi_{\theta_{\text{old}}}(y_t \mid x)},$$

the clipped objective follows standard PPO/GRPO conventions:

$$L_{\text{clip}}(\theta) = -\mathbb{E}\left[ \min\left( r_t(\theta)A_t,\; \text{clip}(r_t(\theta), 1-\epsilon, 1+\epsilon)A_t \right) \right].$$

The clipping threshold $\epsilon$ keeps updates conservative. This safety rail is essential because:
- The underlying base model architecture is compact.
- The hard dataset slices are limited in size.
- The goal is to maximize performance on tail-end hard cases without degrading the high baseline scores established by the SFT model.

---

## 10. Why this remains a challenger, not a guaranteed winner

This distinction must be stated clearly in the final report. The RRPO/DPO hard-mining model is the **most promising RL-style challenger**, but it should not be framed as an absolute replacement for the SFT champion.

### Underlying Factors:
1. The baseline SFT checkpoint is already optimized heavily and scores high across the board.
2. The benchmark evaluation pipeline fixes demonstrated that formatting corrections shift scores significantly, masking some RL policy changes.
3. The remaining failures represent highly subtle edge cases that are difficult to eliminate entirely without larger parameter scales.
4. The active optimization signal is operating on a highly compressed residue of hard cases.

Therefore, the project presents RRPO/DPO as the most mathematically sophisticated and mechanistically aligned refinement framework for future exploration.

---

## 11. Why this is the right final RL story

Including this method in the final submission grounds the narrative. It demonstrates that our training loop design is a direct mathematical response to our mechanistic diagnostics:

$$\text{Latent Competence (Base)} \rightarrow \text{Route Stabilization (SFT)} \rightarrow \text{Coarse Search (GRPO)} \rightarrow \text{Staged Alignment (RRPO/DPO)}.$$

This arc showcases technical depth, tight feedback loops between interpretability and alignment, and rigorous engineering honesty.

---

## 12. Final takeaway

The final RRPO/DPO framework operates under a singular governing principle:

$$\text{The remaining errors are not random. They are structured.}$$

By mirroring that exact structure within the loss formulation via hard-example mining, preference optimization, and layerwise routing constraints, this configuration stands as the project's most principled approach to bridging latent model capability and token execution stability.