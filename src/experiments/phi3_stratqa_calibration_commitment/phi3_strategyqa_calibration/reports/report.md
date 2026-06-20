# StrategyQA commitment / calibration experiment

- Model: `microsoft/phi-3-mini-4k-instruct`
- Validation samples: 200
- Test samples: 200
- Prompt variants: plain, anchored
- Reasoning CoT enabled: True

## Overall results

| Variant | Raw acc | Calibrated acc | Explicit answer rate | Hedged rate | Mean commitment | Threshold | Val acc |
|---|---:|---:|---:|---:|---:|---:|---:|
| plain | 0.185 | 0.510 | 0.260 | 0.000 | 0.571 | -1.5064 | 0.590 |
| anchored | 0.130 | 0.550 | 0.215 | 0.000 | 0.558 | -1.6677 | 0.595 |

## Interpretation hints

- High explicit-answer rate but lower raw accuracy suggests the model commits, but not always correctly.
- A calibrated threshold that improves accuracy suggests the model has useful confidence information.
- High hedging with decent calibrated accuracy suggests the model knows but hesitates.
- Comparing plain vs anchored prompts shows whether the delimiter changes yes/no calibration.