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

## Phi-3 Two-Pass Self-Correction Experiment Results

### GSM8K Performance & Transitions

| Accuracy & Rates | Commitment Analysis |
| :---: | :---: |
| <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/gsm8k_accuracy_bar.png" height="220" alt="GSM8K Accuracy Bar"> | <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/gsm8k_commitment_bar.png" height="220" alt="GSM8K Commitment Bar"> |
| <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/gsm8k_accuracy_line.png" height="220" alt="GSM8K Accuracy Line"> | <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/gsm8k_commitment_delta_hist.png" height="220" alt="GSM8K Commitment Delta Histogram"> |
| <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/gsm8k_transition_rates.png" height="220" alt="GSM8K Transition Rates"> | <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/gsm8k_commitment_hexbin.png" height="220" alt="GSM8K Commitment Hexbin"> |
| <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/gsm8k_transition_heatmap.png" height="220" alt="GSM8K Transition Heatmap"> | <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/gsm8k_commitment_transition_violin.png" height="220" alt="GSM8K Commitment Transition Violin"> |

| Calibration & Diagnostics | Length Distribution |
| :---: | :---: |
| <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/gsm8k_reliability.png" height="220" alt="GSM8K Reliability"> | <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/gsm8k_pass1_length_hist.png" height="220" alt="GSM8K Pass 1 Length Histogram"> |
| <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/gsm8k_metric_correlations.png" height="220" alt="GSM8K Metric Correlations"> | <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/gsm8k_pass2_length_hist.png" height="220" alt="GSM8K Pass 2 Length Histogram"> |

---

### StrategyQA Performance & Transitions

| Accuracy & Rates | Commitment Analysis |
| :---: | :---: |
| <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/strategyqa_accuracy_bar.png" height="220" alt="StrategyQA Accuracy Bar"> | <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/strategyqa_commitment_bar.png" height="220" alt="StrategyQA Commitment Bar"> |
| <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/strategyqa_accuracy_line.png" height="220" alt="StrategyQA Accuracy Line"> | <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/strategyqa_commitment_delta_hist.png" height="220" alt="StrategyQA Commitment Delta Histogram"> |
| <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/strategyqa_transition_rates.png" height="220" alt="StrategyQA Transition Rates"> | <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/strategyqa_commitment_hexbin.png" height="220" alt="StrategyQA Commitment Hexbin"> |
| <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/strategyqa_transition_heatmap.png" height="220" alt="StrategyQA Transition Heatmap"> | <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/strategyqa_commitment_transition_violin.png" height="220" alt="StrategyQA Commitment Transition Violin"> |

| Calibration & Diagnostics | Length Distribution |
| :---: | :---: |
| <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/strategyqa_reliability.png" height="220" alt="StrategyQA Reliability"> | <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/strategyqa_pass1_length_hist.png" height="220" alt="StrategyQA Pass 1 Length Histogram"> |
| <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/strategyqa_metric_correlations.png" height="220" alt="StrategyQA Metric Correlations"> | <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/strategyqa_pass2_length_hist.png" height="220" alt="StrategyQA Pass 2 Length Histogram"> |

---

### Overall Aggregate Metrics

| Accuracy & Rates | Pass 1 vs. Pass 2 Commitment |
| :---: | :---: |
| <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/overall_pass1_accuracy.png" height="220" alt="Overall Pass 1 Accuracy"> | <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/overall_pass1_commitment.png" height="220" alt="Overall Pass 1 Commitment"> |
| <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/overall_pass2_accuracy.png" height="220" alt="Overall Pass 2 Accuracy"> | <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/overall_pass2_commitment.png" height="220" alt="Overall Pass 2 Commitment"> |
| <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/overall_improvement_rate.png" height="220" alt="Overall Improvement Rate"> | |
| <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/overall_regression_rate.png" height="220" alt="Overall Regression Rate"> | |

---

### Task Target Radar Fingerprint

| Overall Task Radar |
| :---: |
| <img src="../../src/experiments/phi3_two_pass_self_correction/phi3_two_pass_self_correction/plots/overall_task_radar.png" height="220" alt="Overall Task Radar"> |

## Conclusion

Self-correction is useful, but only conditionally.  
It should be treated as a controlled mechanism with a verifier, not as an unconditional improvement layer.