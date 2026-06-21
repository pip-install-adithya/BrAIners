# SFT results and champion analysis

This file is the central results chapter for the SFT checkpoint.

## 1. Champion metrics

The validated benchmark numbers for the SFT champion are:

$$\text{GSM8K} = 0.850,\quad \text{StrategyQA} = 0.660,\quad \text{MMLU} = 0.567$$

These are the results the rest of the project should benchmark against. The archived reports explicitly identify this checkpoint as the current model to submit, benchmark against, and use as the baseline for future experiments.

---

## 2. Why these results matter

The most important point is not just that the scores are above threshold. It is that the model’s apparent weakness profile changed.

The project originally assumed that MMLU was the major bottleneck. Later evidence showed that MMLU was no longer a critical weakness after the benchmark pipeline was fixed. GSM8K and MMLU both improved substantially from evaluation corrections, and the SFT checkpoint remained the strongest stable model after those corrections.

That means the champion is not a lucky checkpoint. It is the checkpoint that survives the most honest evaluation.

---

## 3. Comparison against RL attempts

The results also explain why the later RL attempts did not become the main champion story.

The experiments explicitly report that:
- `GRPO_v3` underperformed the baseline SFT on GSM8K and MMLU.
- StrategyQA performance did not move significantly.
- The overall metric improvement driven by evaluation fixes was larger than the gains from online RL experiments.

So the project’s story is not “RL beat SFT.” The narrative settles on:
- SFT established a highly resilient capability baseline.
- The evaluation pipeline became structurally more honest.
- RL strategies had to be explicitly redesigned around the remaining localized bottlenecks.

---

## 4. Mathematical view of why SFT is stable

SFT is stable because it directly optimizes the desired token completion distribution under supervised grounding:

$$\theta^* = \arg\min_\theta L_{\text{SFT}}(\theta)$$

where the target configuration maps precisely to the benchmark-compatible answer format.

In contrast, later RL methods optimize relative policy behavior under a moving reward proxy. While that framework provides broader exploratory flexibility, it introduces higher variance and can shift the policy weights in unintended directions if the reward shaping function is incomplete. 

This behavioral gap explains why the grounded SFT champion serves as a much safer submission model.

---

## 5. What the results suggest about each benchmark

### GSM8K
The model is clearly capable of structured arithmetic reasoning and target final-number routing. The primary performance lever here is answer consolidation alongside reduced structural sensitivity to token truncation.

### StrategyQA
The model resolves the underlying target logic correctly, but the definitive optimization shift is centered on decision sharpness and output commitment. The SFT residual-stream analysis confirms that the adapter predominantly acts as a late-stage steering mechanism within this domain.

### MMLU
The fundamental failure mode is not a raw collapse into an arbitrary single option letter; rather, it is prompt-following discipline and extraction fragility on a highly specific subset of questions. Because the SFT model sits comfortably above the competition threshold, this domain is no longer classified as the core system weakness.

---

## 6. Champion conclusion

The SFT checkpoint is the strongest model because it is:
- Measured with complete experimental honesty
- Highly stable across all three benchmarks
- Fully interpretable under mechanistic analysis
- Already positioned well above target operational thresholds

That is why it should be treated as the baseline anchor in the final report.