# SFT story: why this model became the champion

The plain SFT checkpoint is the most important model in the project because it is the first version that clearly turns the baseline Phi-3-mini into a benchmark-competent reasoning system.

The baseline model already had latent capability, but the early analysis showed that the weak point was not pure knowledge loss. It was the interface between reasoning and final answer emission. That is exactly the kind of issue SFT can improve when the data, formatting, and extraction pipeline are designed well.

The project’s benchmark history makes this very clear. Earlier evaluation fixes moved GSM8K from 0.280 to 0.760 and MMLU from 0.220 to 0.453 without changing model weights, and the later validated SFT pipeline reached GSM8K 0.850, StrategyQA 0.660, and MMLU 0.567. That is why the project now treats SFT as the stable champion. 

## Core interpretation

SFT did not simply “make the model smarter.”
It made the model more usable:
- it improved answer routing,
- it improved output discipline,
- it improved task-specific commitment,
- and it reduced the dependence on brittle extraction behavior.

This is especially visible in the TLens analysis. On GSM8K, the SFT model more cleanly routes internal evidence into the final numeric slot and suppresses scaffold tokens near the end. On StrategyQA, the SFT model shows a cleaner decision collapse and stronger late-stage commitment. 

## Why that matters for the whole project

The later RL experiments are only interpretable because the SFT model is already strong.
Once SFT is established as the champion, the question becomes:
- can RL improve on top of a strong checkpoint?
- or does RL mostly change reward shape without beating the champion?

The project’s evidence says that the second question is the harder one. The champion model already clears the required thresholds and provides the correct baseline for future comparison. 

## Final statement

SFT is the model you should submit as the safest solution because it is the strongest checkpoint that is still stable, reproducible, and easy to justify mechanistically.