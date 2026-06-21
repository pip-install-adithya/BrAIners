# GRPO failure analysis

This file explains why the initial GRPO-style attempts did not become the final solution.

## 1. Objective mismatch

The main reason is that the reward function was too weakly aligned with the actual benchmark behavior.

A policy may maximize expected reward

$$\max_\theta \mathbb{E}_{y \sim \pi_\theta}[R(x,y)],$$

yet still fail to maximize benchmark accuracy if the reward does not encode the true failure modes.

That is what happened here.

The model’s real bottlenecks were:
- Late answer routing
- Calibration
- Format compliance
- Task-specific emission behavior

A generic reward signal cannot fully capture all of that.

## 2. Reward did not fully represent the task

A completion that is:
- Semantically close
- But poorly formatted
- Or overly confident too early
- Or structurally biased toward a certain answer slot

may still receive a reward that is too high relative to its actual benchmark value.

So the optimization target becomes:

$$R_{\text{proxy}}(x,y),$$

instead of the true desired target:

$$R_{\text{task}}(x,y).$$

That difference is enough to explain why reward and accuracy can decouple.

## 3. Task asymmetry

The tasks are not identical.

- GSM8K needs correct final-number routing.
- StrategyQA needs calibration and commitment.
- MMLU needs answer-slot invariance and clean option selection.

A single flat reward cannot treat all three equally well.

This is one reason the GRPO family was not enough on its own.

## 4. Why this is not a negative result

This phase is scientifically useful because it shows the boundaries of generic RL.

It tells us that:
- The policy can improve in local ways
- But the real bottleneck is more structured than a generic reward loop assumes

That is exactly what the later hierarchical and hard-mined methods are designed to handle.

## 5. Mechanistic interpretation

The TLens evidence suggests that the model’s computation is phase-like:
- Evidence accumulation in earlier layers
- Answer shaping in the middle
- Final commitment in the late layers

If the reward does not explicitly care about that phase structure, then the policy can optimize the wrong part of the trajectory.

That is why the GRPO family was useful as a baseline but not as the final method.

## 6. Summary

The failure is best understood as:

$$\text{better reward} \not\Rightarrow \text{better benchmark}$$

unless the reward is aligned with the actual answer-routing and calibration bottlenecks.

That insight is the bridge to hierarchical steering and RRPO/DPO.