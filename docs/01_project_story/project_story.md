# Project story: from baseline failures to mechanistic reasoning control

## 1. What the competition asked for

The project was not just to maximize benchmark scores. The real goal was to build an AI reasoning system that is technically sound, experimentally grounded, and well documented. That meant the work had to demonstrate:
- a working prototype,
- explicit reasoning about failure modes,
- a visible improvement path,
- and a strong enough narrative to justify the chosen solution.

That is why the project is structured around diagnostics first, then intervention design, then controlled refinement.

## 2. What the raw model looked like

The raw Phi-3-mini baseline had three very different failure profiles:
- GSM8K: it often reasoned for a long time but failed on arithmetic closure, premature stopping, or final-number extraction.
- StrategyQA: it often knew the answer but did not always emit an explicit `yes`/`no`.
- MMLU: it was highly sensitive to answer formatting and selection mechanics, and could look much worse than it really was if extraction was naïve.

The baseline was therefore not a single “bad model” story. It was a mixture of:
- reasoning weakness,
- format weakness,
- calibration weakness,
- and parser sensitivity.

## 3. What changed the scores the most

The biggest score jumps came from fixing evaluation, not from training alone.

The archives and the reports show that:
- a naïve MMLU evaluation could dramatically undercount the model because answer extraction was too brittle;
- a GSM8K run could look weak if generation was truncated too early;
- a StrategyQA run could look weak if empty answers were treated as wrong without calibration.

Once the evaluation pipeline was corrected, the model’s measured performance moved substantially upward:
- GSM8K rose into a strong range,
- StrategyQA became respectable and stable,
- MMLU crossed the competition target on the selected hard subset.

That result matters because it means the model already had much more usable signal than the earliest numbers suggested.

## 4. What the mechanistic experiments revealed

The interpretability work made the project much more interesting than a raw benchmark run.

The TLens-style dashboards showed that:
- the residual stream grows strongly in the later layers;
- answer salience typically emerges late;
- the final answer token is often a routing problem rather than a knowledge problem;
- prompt syntax can redirect computation;
- and task families occupy different representational regions.

This was the key turning point. It suggested that the next improvements should not come from “more generic RL,” but from interventions that are aware of:
- when the model decides,
- how it finalizes,
- how it calibrates,
- and how it routes task-specific information.

## 5. Why the final solution is split into two models

The final submission story is deliberately conservative and honest.

### Plain SFT champion
This is the safest model:
- it is stable,
- it already performs well,
- and it is the least likely to lose capability from over-optimization.

### RRPO hard-mining challenger
This is the more novel model:
- it focuses on what is still broken,
- it uses hard-example mining,
- it includes routing-aware reward shaping,
- and it is designed to be a targeted improvement rather than a broad rewrite.

The project therefore does not pretend that RL “won” in a simple sense.  
Instead, it shows a strong baseline, a mechanistic diagnosis, and a more ambitious challenger that is justified by the failure modes.

## 6. The core thesis

Phi-3-mini already has enough latent ability to solve a large fraction of these tasks.  
The bottleneck is the interface between latent reasoning and final answer emission.

That means the best interventions are not:
- blind scaling,
- generic reward hacking,
- or oversized fine-tuning.

The best interventions are:
- better answer routing,
- better calibration,
- better prompt discipline,
- better extraction,
- and targeted training on the examples that still fail.

That thesis is the backbone of the entire project.