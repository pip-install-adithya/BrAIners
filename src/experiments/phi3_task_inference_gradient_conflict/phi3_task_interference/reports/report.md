# Task interference / gradient conflict report

- Model: `microsoft/phi-3-mini-4k-instruct`
- Tasks: gsm8k, strategyqa, mmlu
- GSM8K samples: 5
- StrategyQA samples: 5
- MMLU samples per subject: 3
- MMLU subjects: abstract_algebra, college_mathematics, logical_fallacies
- Gradient layers: [26, 27, 28, 29, 30, 31]
- Representation layers: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]...

## Evaluation summary

| Task | Greedy accuracy | Mean loss | Std loss | Mean prompt tokens | Mean completion tokens |
|---|---:|---:|---:|---:|---:|
| gsm8k | 0.200 | 0.385 | 0.171 | 86.6 | 64.4 |
| strategyqa | 0.400 | 9.286 | 0.899 | 22.6 | 16.6 |
| mmlu | 0.556 | 7.124 | 4.166 | 88.7 | 16.2 |

## Gradient conflict summary

| Task A | Task B | Cosine | Dot | Conflict |
|---|---|---:|---:|---|
| gsm8k | strategyqa | nan | 0.0000e+00 | False |
| gsm8k | mmlu | nan | 0.0000e+00 | False |
| strategyqa | mmlu | nan | 0.0000e+00 | False |

## PCGrad simulation

- Naive combined norm: 0.0000
- PCGrad combined norm: 0.0000
- Pairwise negative gradient pairs: 0

## Representation overlap summary

| Task A | Task B | Mean subspace overlap | Mean centroid cosine | Mean CKA |
|---|---|---:|---:|---:|
| gsm8k | strategyqa | 0.1254 | 0.8495 | 0.4704 |
| gsm8k | mmlu | 0.1746 | 0.9515 | 0.5197 |
| strategyqa | gsm8k | nan | nan | nan |
| strategyqa | mmlu | 0.2156 | 0.9471 | 0.7425 |
| mmlu | gsm8k | nan | nan | nan |
| mmlu | strategyqa | nan | nan | nan |

## Why this matters

- Negative task-gradient cosine suggests cross-task interference in shared layers.
- Lower representation overlap indicates the tasks occupy different subspaces, supporting routing / adapters.
- PCGrad reduces direct gradient conflict without changing the model.
- The MMLU delimiter run can be compared against the plain baseline to see whether formatting changes the interference pattern.