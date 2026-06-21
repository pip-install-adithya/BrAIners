# GRPO attempts

This file documents the broad GRPO-style exploration phase.

## 1. The reason this phase was introduced

The early evidence suggested that the model’s main weakness was not a complete lack of reasoning ability.  
Instead, it seemed to struggle with how reasoning becomes a final answer.

That means a group-relative policy update was worth trying.

Given a prompt $x$, sample completions $y_1, y_2, \dots, y_K$ from the policy:

$$y_k \sim \pi_\theta(\cdot \mid x).$$

Then score each completion using a reward function:

$$R_k = R(x, y_k).$$

A normalized advantage can be defined as:

$$A_k = \frac{R_k - \mu_R}{\sigma_R + \epsilon}, \quad \mu_R = \frac{1}{K}\sum_{j=1}^{K} R_j.$$

This setup is attractive because it can reward the best trajectory among several candidates instead of forcing the model to learn from only one sample.

## 2. What the objective was trying to do

The generic policy-gradient form can be written as

$$L_{\text{PG}}(\theta) = -\mathbb{E}\left[A_k \log \pi_\theta(y_k \mid x)\right].$$

A clipped version is often more stable:

$$L_{\text{clip}}(\theta) = -\mathbb{E}\left[ \min\left( r_k(\theta)A_k,\; \mathrm{clip}(r_k(\theta), 1-\epsilon, 1+\epsilon)A_k \right) \right],$$

where

$$r_k(\theta)=\frac{\pi_\theta(y_k\mid x)}{\pi_{\theta_{\text{old}}}(y_k\mid x)}.$$

The intuition was simple:
- Reward better candidates
- Suppress weaker ones
- Move the policy toward the better answer routes

## 3. Why that seemed plausible from the mechanistic results

The TLens work showed that answer salience tends to emerge late in the stack.  
If the network already has a structured latent route, then a relative reward objective should be able to reinforce that route.

The reasoning was:

$$\text{internal evidence} + \text{better routing pressure} \longrightarrow \text{better final answers}.$$

## 4. What happened in practice

The GRPO family often improved reward, but not the benchmark scores enough to beat the plain SFT checkpoint consistently.

This means the policy learned something useful about the reward function, but not enough about the true task objective.

The mismatch can be viewed as:

$$R(x,y) \not\equiv \text{benchmark correctness}.$$

That is why a reward gain was not sufficient.

## 5. Why this phase still mattered

This phase established three important facts:

1. The model is trainable by RL.
2. The RL signal can move the policy.
3. Generic GRPO is too coarse to solve the project alone.

That last point is the most valuable.  
It tells us that the training objective needs to be more aligned with:
- Calibration
- Commitment
- Answer-slot stability
- Task-specific structure