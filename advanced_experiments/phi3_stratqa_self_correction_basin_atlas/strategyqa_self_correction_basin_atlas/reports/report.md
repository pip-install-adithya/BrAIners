# StrategyQA self-correction basin atlas report

- Model: `microsoft/phi-3-mini-4k-instruct`
- Validation samples: 120
- Test samples: 120
- Prompt variants: plain, anchored, anchored_reason, anchored_xml, anchored_selfcheck, answer_first, verbose
- Baseline variant: `plain`
- Deterministic decoding: True

## Overall summary

| Metric | Value |
|---|---:|
| n_questions | 120.000 |
| n_variants | 7.000 |
| baseline_variant | plain |
| baseline_pass1_raw_accuracy | 0.450 |
| baseline_pass2_raw_accuracy | 0.425 |
| baseline_pass1_cal_accuracy | 0.583 |
| baseline_pass2_cal_accuracy | 0.592 |
| baseline_improvement_rate | 0.125 |
| baseline_regression_rate | 0.150 |
| baseline_transition_entropy | 1.831 |
| baseline_q_stability_mean | 0.642 |
| baseline_q_drift_mean | 0.303 |

## Variant summary

| Variant | Pass1 acc | Pass2 acc | Pass1 cal acc | Pass2 cal acc | Improve | Regress | Transition entropy | Drift |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| plain | 0.450 | 0.425 | 0.583 | 0.592 | 0.125 | 0.150 | 1.831 | 0.303 |
| anchored | 0.567 | 0.558 | 0.558 | 0.558 | 0.050 | 0.058 | 1.482 | 0.063 |
| anchored_reason | 0.625 | 0.600 | 0.633 | 0.608 | 0.117 | 0.142 | 1.772 | 0.154 |
| answer_first | 0.467 | 0.233 | 0.608 | 0.525 | 0.042 | 0.275 | 1.664 | 0.312 |
| anchored_xml | 0.550 | 0.525 | 0.558 | 0.542 | 0.142 | 0.167 | 1.884 | 0.171 |
| anchored_selfcheck | 0.600 | 0.558 | 0.567 | 0.542 | 0.133 | 0.175 | 1.861 | 0.247 |
| verbose | 0.617 | 0.508 | 0.542 | 0.558 | 0.150 | 0.258 | 1.935 | 0.156 |

## Question basin classes

| Basin class | Count |
|---|---:|
| moderately stable basin | 53 |
| stable correct basin | 33 |
| uncertain basin | 17 |
| stable but diverse basin | 10 |
| flip-prone basin | 7 |

## Interpretation

- A high stability score means the question rarely flips across prompt variants and passes.
- A high transition entropy means the sample moves through many different states (e.g. wrong→correct, correct→wrong).
- The phase portraits show whether pass2 sharpens or destabilizes the decision basin.
- The quiver map shows the direction of self-correction in confidence-commitment space.
- The improvement and regression basins reveal where self-correction is genuinely helpful and where it over-corrects.
- The response-drift plots show whether explanation drift aligns with confidence changes.
- The glyph atlas makes individual question behavior visually inspectable at a glance.