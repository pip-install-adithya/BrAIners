# Two-pass self-correction experiment report

- Model: `microsoft/phi-3-mini-4k-instruct`
- Tasks: gsm8k, strategyqa
- Pass-1 max new tokens: {'gsm8k': 256, 'strategyqa': 48, 'mmlu': 48}
- Pass-2 max new tokens: {'gsm8k': 256, 'strategyqa': 48, 'mmlu': 48}
- Temperature: 0.7
- Top-p: 0.9
- Few-shot enabled: True

## Summary table

| Task | Pass 1 acc | Pass 2 acc | Improve | Regress | Unchanged |
|---|---:|---:|---:|---:|---:|
| gsm8k | 0.500 | 0.300 | 0.033 | 0.233 | 0.733 |
| strategyqa | 0.667 | 0.500 | 0.083 | 0.250 | 0.667 |

## Interpretation hints

- Improvement cases justify the self-correction / process-reward direction.
- Regression cases show where the critique pass destabilizes already-correct answers.
- If the commit score rises in improved samples, the model is learning to be more decisive after review.
- Transition matrices show whether pass-2 mostly fixes wrong answers or also flips correct ones.
- The calibration-style reliability plots indicate whether the pass-2 commitment score tracks actual correctness.