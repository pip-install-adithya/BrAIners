# Hierarchical Steering GRPO

This file documents the more structured RL variant.

## 1. Why hierarchical steering was introduced

The mechanistic work showed that the model does not make its decision in one flat step.  
It evolves through stages.

So the training objective should also be staged.

If we write the completion process as layers or phases $p = 1,\dots,P$, then a hierarchical reward can be written as

$$R_{\text{hier}}(x,y) = \sum_{p=1}^{P} \alpha_p R_p(x,y),$$

where later phases may get larger weights.

That idea is consistent with the TLens result that late answer routing is the decisive bottleneck.

## 2. What the hierarchy is trying to model

The hierarchy is conceptually:

1. **Early stabilization**  
   Keep the reasoning trajectory coherent
2. **Mid-course consistency**  
   Reduce drift and contradiction
3. **Late answer commitment**  
   Push the correct final answer token
4. **Format compliance**  
   Ensure the answer is benchmark-readable

That structure reflects what the interpretability work found.

## 3. Why this is better than flat GRPO

A flat reward assumes all parts of the completion matter equally.  
But the TLens plots showed that the answer token is usually decided late.

So if the model is optimized by

$$L_{\text{flat}} = -\mathbb{E}[R(x,y)\log \pi_\theta(y|x)],$$

it may spend too much effort on the wrong phase.

A hierarchical objective can instead emphasize a late-stage routing term such as

$$L_{\text{route}} = \sum_{\ell \in \mathcal{L}_{\text{late}}} \left(p_\ell - \tau_\ell\right)^2,$$

where $p_\ell$ is the probability assigned to the target answer token at layer $\ell$, and $\tau_\ell$ is a target curve that rises only in the later layers.

This is much closer to the observed behavior.

## 4. Why it was worth trying

The advanced experiments showed that:
- Prompt structure changes the answer path
- StrategyQA behaves like a calibration basin
- MMLU is sensitive to option order
- GSM8K needs a clean late-stage consolidation

Hierarchical steering was designed to exploit that structure rather than ignore it.

## 5. What the results suggested

The model became more controlled, but the gains were still not enough to clearly displace the strong SFT champion.

That means the model is steerable, but the policy update still needs to be more selective about what it trains on.

## 6. Interpretation

Hierarchical steering is best seen as a bridge between generic GRPO and the final RRPO/DPO design.

It adds two important ideas:
- Not all tokens are equally important
- Not all phases of the completion should receive equal reward pressure

That is a much more realistic model of how the task is actually solved.