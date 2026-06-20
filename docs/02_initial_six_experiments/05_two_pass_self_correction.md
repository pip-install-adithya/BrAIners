# Two-pass self-correction experiment

This experiment asks whether the model improves when it gets a second reasoning pass to inspect its own answer.

## Experimental setup

- Model: `microsoft/phi-3-mini-4k-instruct`
- Tasks: GSM8K and StrategyQA
- Pass-1 max new tokens:
  - GSM8K: 256
  - StrategyQA: 48
- Pass-2 max new tokens:
  - GSM8K: 256
  - StrategyQA: 48
- Temperature: 0.7
- Top-p: 0.9
- Few-shot: enabled

## Main results

| Task | Pass 1 acc | Pass 2 acc | Improve | Regress | Unchanged |
|---|---:|---:|---:|---:|---:|
| gsm8k | 0.500 | 0.300 | 0.033 | 0.233 | 0.733 |
| strategyqa | 0.667 | 0.500 | 0.083 | 0.250 | 0.667 |

## Interpretation

The main lesson is that self-correction is not a free win.

- Some samples improve.
- Some regress.
- Many stay unchanged.
- The second pass often changes verbosity more than decision quality.

That means the model is not yet a robust self-verifier.  
It can revise, but revision is not reliably beneficial.

This is still useful.  
It shows that process-level rewards and self-correction mechanisms are worth investigating, but they need routing, selection, or a verifier.  
Otherwise, the second pass can destabilize correct answers.

## Figures to embed

- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/overall_improvement_rate.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/overall_regression_rate.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/overall_pass1_accuracy.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/overall_pass2_accuracy.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/overall_pass1_commitment.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/overall_pass2_commitment.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/overall_task_radar.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/gsm8k_accuracy_bar.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/gsm8k_accuracy_line.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/gsm8k_commitment_bar.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/gsm8k_commitment_delta_hist.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/gsm8k_commitment_hexbin.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/gsm8k_commitment_transition_violin.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/gsm8k_metric_correlations.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/gsm8k_pass1_length_hist.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/gsm8k_pass2_length_hist.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/gsm8k_reliability.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/gsm8k_transition_heatmap.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/gsm8k_transition_rates.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/strategyqa_accuracy_bar.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/strategyqa_accuracy_line.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/strategyqa_commitment_bar.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/strategyqa_commitment_delta_hist.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/strategyqa_commitment_hexbin.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/strategyqa_commitment_transition_violin.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/strategyqa_metric_correlations.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/strategyqa_pass1_length_hist.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/strategyqa_pass2_length_hist.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/strategyqa_reliability.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/strategyqa_transition_heatmap.png`
- `../experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/strategyqa_transition_rates.png`

## Conclusion

Self-correction is useful, but only conditionally.  
It should be treated as a controlled mechanism with a verifier, not as an unconditional improvement layer.