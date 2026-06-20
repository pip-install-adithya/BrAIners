# Phi-3 residual stream analysis — deep_insights SFT run

This chapter is the main TLens chapter for the submission.  
It is the more polished version of the SFT comparison and should be treated as the canonical residual-stream reference in the report.

## Main question

How does the SFT checkpoint reshape the model’s late-layer answer routing, confidence collapse, and token-level decision geometry?

## What the analysis shows

The same broad conclusion appears again, but more clearly:
- the base model already contains rich latent structure,
- SFT does not erase that structure,
- but SFT makes the answer route more decisive,
- and the final answer token becomes easier to separate from the rest of the trajectory.

The comparison dashboards are especially important because they make the story legible at a glance:
- residual norm overlay,
- cosine-to-final overlay,
- PCA trajectory comparison,
- and a compact summary table for each sample.

## Why this version matters

The five advanced experiments show that the project is not about a single trick:
- prompt shape matters,
- calibration matters,
- permutation order matters,
- self-correction is conditional,
- and task geometry is different across benchmark families.

This SFT TLens chapter sits after those studies and acts as the synthesis point: it shows that the best supervised checkpoint is the one that most cleanly routes internal computation into the final answer. That is why this is the right TLens reference for the final submission narrative.

## Report-level takeaway

The deep_insights archive should be used to justify the following claim:

**The strongest SFT checkpoint improves answer commitment more than it changes the early reasoning path.**

That claim is consistent with the earlier diagnostics and gives a direct mechanistic reason to keep the plain SFT model as the submission champion.

## Figures to embed

- `../phi3_residual_stream_deep_insights/plots/accuracy_comparison.png`
- `../phi3_residual_stream_deep_insights/plots/base/gsm8k_0_dashboard.png`
- `../phi3_residual_stream_deep_insights/plots/base/gsm8k_1_dashboard.png`
- `../phi3_residual_stream_deep_insights/plots/base/strategyqa_0_dashboard.png`
- `../phi3_residual_stream_deep_insights/plots/base/strategyqa_1_dashboard.png`
- `../phi3_residual_stream_deep_insights/plots/sft/gsm8k_0_dashboard.png`
- `../phi3_residual_stream_deep_insights/plots/sft/gsm8k_1_dashboard.png`
- `../phi3_residual_stream_deep_insights/plots/sft/strategyqa_0_dashboard.png`
- `../phi3_residual_stream_deep_insights/plots/sft/strategyqa_1_dashboard.png`
- `../phi3_residual_stream_deep_insights/plots/comparison/gsm8k_0_comparison.png`
- `../phi3_residual_stream_deep_insights/plots/comparison/gsm8k_0_sequence_dynamics.png`
- `../phi3_residual_stream_deep_insights/plots/comparison/gsm8k_1_comparison.png`
- `../phi3_residual_stream_deep_insights/plots/comparison/gsm8k_1_sequence_dynamics.png`
- `../phi3_residual_stream_deep_insights/plots/comparison/strategyqa_0_comparison.png`
- `../phi3_residual_stream_deep_insights/plots/comparison/strategyqa_0_sequence_dynamics.png`
- `../phi3_residual_stream_deep_insights/plots/comparison/strategyqa_1_comparison.png`
- `../phi3_residual_stream_deep_insights/plots/comparison/strategyqa_1_sequence_dynamics.png`

## Closing line

This is the version that should be cited in the main report when explaining why SFT is the stable champion. 