# StrategyQA calibration / commitment experiment

This experiment treats StrategyQA as a calibration problem rather than a pure knowledge problem.

## Experimental setup

- Model: `microsoft/phi-3-mini-4k-instruct`
- Validation samples: 200
- Test samples: 200
- Prompt variants: plain, anchored
- CoT enabled: yes

## Main results

| Variant | Raw acc | Calibrated acc | Explicit answer rate | Hedged rate | Mean commitment | Threshold | Val acc |
|---|---:|---:|---:|---:|---:|---:|---:|
| plain | 0.185 | 0.510 | 0.260 | 0.000 | 0.571 | -1.5064 | 0.590 |
| anchored | 0.130 | 0.550 | 0.215 | 0.000 | 0.558 | -1.6677 | 0.595 |

The important result is that calibration helps a lot more than raw text scoring suggests.

## Interpretation

StrategyQA is not mainly failing because the model is clueless.  
It is failing because the model:
- does not always commit clearly,
- can output an answer that is hard to parse,
- and benefits from threshold-based calibration.

The calibrated score is much more informative than the raw one.  
That means the latent model signal is real, but the surface text is unreliable.

This is also why later training and evaluation used:
- a stronger answer-finalization format,
- clearer `yes` / `no` anchoring,
- and explicit commitment analysis.

The anchored prompt improves calibrated behavior, but the effect is not identical to raw accuracy.  
That distinction matters: the model can be more usable even if the raw string is still noisy.

## Figures to embed

- `../experiments/phi3_stratqa_calibration_commitment/phi3_strategyqa_calibration/plots/accuracy_bar_plain.png`
- `../experiments/phi3_stratqa_calibration_commitment/phi3_strategyqa_calibration/plots/accuracy_bar_anchored.png`
- `../experiments/phi3_stratqa_calibration_commitment/phi3_strategyqa_calibration/plots/commitment_bar_plain.png`
- `../experiments/phi3_stratqa_calibration_commitment/phi3_strategyqa_calibration/plots/commitment_bar_anchored.png`
- `../experiments/phi3_stratqa_calibration_commitment/phi3_strategyqa_calibration/plots/commitment_hist_plain.png`
- `../experiments/phi3_stratqa_calibration_commitment/phi3_strategyqa_calibration/plots/commitment_hist_anchored.png`
- `../experiments/phi3_stratqa_calibration_commitment/phi3_strategyqa_calibration/plots/completion_length_plain.png`
- `../experiments/phi3_stratqa_calibration_commitment/phi3_strategyqa_calibration/plots/completion_length_anchored.png`
- `../experiments/phi3_stratqa_calibration_commitment/phi3_strategyqa_calibration/plots/logodds_hist_plain.png`
- `../experiments/phi3_stratqa_calibration_commitment/phi3_strategyqa_calibration/plots/logodds_hist_anchored.png`
- `../experiments/phi3_stratqa_calibration_commitment/phi3_strategyqa_calibration/plots/logodds_violin_by_class_plain.png`
- `../experiments/phi3_stratqa_calibration_commitment/phi3_strategyqa_calibration/plots/logodds_violin_by_class_anchored.png`
- `../experiments/phi3_stratqa_calibration_commitment/phi3_strategyqa_calibration/plots/logodds_vs_commitment_hexbin_plain.png`
- `../experiments/phi3_stratqa_calibration_commitment/phi3_strategyqa_calibration/plots/logodds_vs_commitment_hexbin_anchored.png`
- `../experiments/phi3_stratqa_calibration_commitment/phi3_strategyqa_calibration/plots/reliability_plain.png`
- `../experiments/phi3_stratqa_calibration_commitment/phi3_strategyqa_calibration/plots/reliability_anchored.png`
- `../experiments/phi3_stratqa_calibration_commitment/phi3_strategyqa_calibration/plots/threshold_search_plain.png`
- `../experiments/phi3_stratqa_calibration_commitment/phi3_strategyqa_calibration/plots/threshold_search_anchored.png`
- `../experiments/phi3_stratqa_calibration_commitment/phi3_strategyqa_calibration/plots/metric_correlations_plain.png`
- `../experiments/phi3_stratqa_calibration_commitment/phi3_strategyqa_calibration/plots/metric_correlations_anchored.png`
- `../experiments/phi3_stratqa_calibration_commitment/phi3_strategyqa_calibration/plots/variant_performance_radar.png`

## Conclusion

StrategyQA is a commitment problem first and a reasoning problem second.  
That is why calibration-aware decoding is one of the strongest low-cost interventions in the project.