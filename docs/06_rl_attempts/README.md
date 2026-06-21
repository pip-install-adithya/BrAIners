# RL Attempts

This folder documents the reinforcement-learning exploration path of the project.

The RL story is not a simple success story.  
It is a sequence of increasingly structured optimization attempts, each one designed in response to the failure modes identified by the benchmark work and the mechanistic interpretability results.

## Core training view

Let the policy be $\pi_\theta$, the prompt be $x$, and a completion be $y$.  
The general RL objective can be written as

$$J(\theta) = \mathbb{E}_{y \sim \pi_\theta(\cdot \mid x)}[R(x,y)],$$

where $R(x,y)$ is a task reward that ideally measures correctness, format compliance, and answer-routing quality.

In practice, the project found that a single undifferentiated reward was too coarse.  
The model did not fail in one uniform way.  
It failed through:
- Late answer-routing instability
- Calibration problems
- Option-order bias
- Format fragility
- Task-specific bottlenecks

So the RL exploration evolved in stages.

## Folder structure

* **`01_grpo_family/`**
  - Broad GRPO-style attempts
  - Why they were tried
  - Why they did not become the final solution
* **`02_hierarchical_steering_grpo.md`**
  - The more structured steering-based RL variant
  - The stage-aware reward design
  - The reason it improved behavior but still did not fully beat SFT
* **`03_rrpo_dpo.md`**
  - The final hard-mining, routing-aware challenger
  - The DPO-style preference formulation
  - The rationale for making the training objective more selective
* **`04_rl_attempts_figure_index.md`**
  - All figure paths and their role in the RL narrative

## Why this folder matters

The earlier TLens and advanced mechanistic experiments showed that the model already had latent reasoning ability.  
The bottleneck was not “does the model know anything?”  
The bottleneck was closer to:

$$\text{reasoning state} \longrightarrow \text{stable answer emission}.$$

This folder is where that insight becomes a training design.

## High-level conclusion

The RL attempts were valuable even when they did not outperform the plain SFT champion.  
They showed that:
- Generic RL is not enough
- Stage-aware steering is more aligned with the failure modes
- Hard-example mining plus preference optimization is the most principled RL-style challenger

The plain SFT checkpoint remains the stable champion.  
The RRPO/DPO-style model is the strongest RL challenger.