# GRPO Family

This subfolder contains the first RL exploration phase.

The basic hypothesis was:

$$\text{If the model already has latent reasoning ability, then a group-relative reward objective should improve benchmark behavior.}$$

That hypothesis was reasonable because the mechanistic evidence showed that the model often had useful internal state, but struggled with final routing and commitment.

In other words, the model frequently looked like it was solving an internal subproblem correctly, but failing at the last transformation into a benchmark-compatible answer.

## Why GRPO was tried

A GRPO-style objective is attractive because it compares multiple candidate rollouts for the same prompt.

If a prompt $x$ generates candidates $y_1,\dots,y_K$, then one can define a relative advantage such as

$$A_k = R(x,y_k) - \frac{1}{K}\sum_{j=1}^{K} R(x,y_j),$$

and update the policy toward the better candidates.

This seemed appropriate because the project’s failures were often relative:
- One rollout is cleaner than another
- One answer is better formatted than another
- One reasoning path commits more reliably than another

## What this phase was meant to test

- Can group-relative reward improve answer routing?
- Can a simple RL loop increase reliability on GSM8K, StrategyQA, and MMLU?
- Can the policy learn to prefer better completion shapes?

## What the experiments showed

The training loop was often stable, but benchmark gains were not consistent.  
That means the model could optimize the reward proxy without consistently improving the final benchmark metric.

This is an important result because it suggests a mismatch between:

$$R(x,y) \quad \text{and} \quad \text{true benchmark correctness}.$$

## Interpretation

The GRPO family was the first sign that the model is steerable, but not automatically in the right direction.

That is why later stages became more structured:
- Hierarchical steering
- Routing-aware shaping
- Hard-example mining
- Preference optimization

The GRPO family is therefore not a failed idea.  
It is the necessary first RL baseline.