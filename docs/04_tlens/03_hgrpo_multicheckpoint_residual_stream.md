# Phi-3 residual stream analysis — HGRPO multicheckpoint run

This chapter is the training-trajectory counterpart to the SFT TLens chapter.  
Instead of comparing only the base model and the final checkpoint, it tracks how the residual stream changes across the HGRPO progression.

## Main question

How does the model evolve across checkpoints, and does the late-layer routing improve steadily or simply shift in a different direction?

## What this archive adds

The checkpoint view is valuable because it shows dynamics rather than just endpoints:
- base checkpoint,
- checkpoint-150,
- checkpoint-200,
- checkpoint-250,
- final_model.

This makes the training story more interpretable:
- some layers move early,
- some answer routes become more visible later,
- and the model’s behavior can change without producing a clean accuracy breakthrough.

## How to read the plots

The most important plot is the accuracy progression figure.  
It should be read alongside the checkpoint dashboards and sequence-dynamics figures. Together, they show whether the model is:
- converging,
- over-committing,
- flattening into a single route,
- or changing the answer path without truly improving robustness.

## Mechanistic interpretation

The HGRPO run is useful because it confirms a key theme from the earlier experiments:
optimizing for reward alone does not guarantee better final reasoning behavior.

In the checkpoint dashboards, what often changes most visibly is:
- the confidence profile,
- the output structure,
- and the late-stage residual routing.

That is interesting, but not automatically enough to outperform the strong SFT model on all benchmarks.

## Report-level takeaway

This archive should be presented as a **useful mechanistic progression**, not as the final solution. It is evidence that the model is highly steerable, but the steerability does not always translate into a clean benchmark win.

That is exactly why the project’s final story stays honest:
- SFT is the reliable champion,
- HGRPO is the training-trajectory proof that the model can be moved,
- and RRPO hard-mining is the most promising next-step challenger.

## Figures to embed

- `../phi3_residual_stream_deep_insights/plots/accuracy_progression.png`

### Base dashboards
- `../phi3_residual_stream_deep_insights/plots/base/gsm8k_0_dashboard.png`
- `../phi3_residual_stream_deep_insights/plots/base/gsm8k_1_dashboard.png`
- `../phi3_residual_stream_deep_insights/plots/base/strategyqa_0_dashboard.png`
- `../phi3_residual_stream_deep_insights/plots/base/strategyqa_1_dashboard.png`

### Checkpoint-150 dashboards
- `../phi3_residual_stream_deep_insights/plots/checkpoint-150/gsm8k_0_dashboard.png`
- `../phi3_residual_stream_deep_insights/plots/checkpoint-150/gsm8k_1_dashboard.png`
- `../phi3_residual_stream_deep_insights/plots/checkpoint-150/strategyqa_0_dashboard.png`
- `../phi3_residual_stream_deep_insights/plots/checkpoint-150/strategyqa_1_dashboard.png`

### Checkpoint-200 dashboards
- `../phi3_residual_stream_deep_insights/plots/checkpoint-200/gsm8k_0_dashboard.png`
- `../phi3_residual_stream_deep_insights/plots/checkpoint-200/gsm8k_1_dashboard.png`
- `../phi3_residual_stream_deep_insights/plots/checkpoint-200/strategyqa_0_dashboard.png`
- `../phi3_residual_stream_deep_insights/plots/checkpoint-200/strategyqa_1_dashboard.png`

### Checkpoint-250 dashboards
- `../phi3_residual_stream_deep_insights/plots/checkpoint-250/gsm8k_0_dashboard.png`
- `../phi3_residual_stream_deep_insights/plots/checkpoint-250/gsm8k_1_dashboard.png`
- `../phi3_residual_stream_deep_insights/plots/checkpoint-250/strategyqa_0_dashboard.png`
- `../phi3_residual_stream_deep_insights/plots/checkpoint-250/strategyqa_1_dashboard.png`

### Final-model dashboards
- `../phi3_residual_stream_deep_insights/plots/final_model/gsm8k_0_dashboard.png`
- `../phi3_residual_stream_deep_insights/plots/final_model/gsm8k_1_dashboard.png`
- `../phi3_residual_stream_deep_insights/plots/final_model/strategyqa_0_dashboard.png`
- `../phi3_residual_stream_deep_insights/plots/final_model/strategyqa_1_dashboard.png`

### Comparison and sequence-dynamics folders
For each sample id shown in the archive, keep the corresponding:
- `*_comparison_*.png`
- `*_sequence_dynamics_*.png`

The sample IDs visible in the TLens archive are:
- `gsm8k_0`
- `gsm8k_1`
- `strategyqa_0`
- `strategyqa_1`

## Closing line

This chapter is the bridge between training and mechanistic diagnosis: it shows what the model changed into, not only whether it improved.