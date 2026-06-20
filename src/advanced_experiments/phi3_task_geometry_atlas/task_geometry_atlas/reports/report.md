# Task geometry atlas report

- Model: `microsoft/phi-3-mini-4k-instruct`
- Samples: GSM8K=30, StrategyQA=30, MMLU per subject=12
- Subjects: abstract_algebra, college_mathematics, logical_fallacies, formal_logic, high_school_mathematics

## Task summary

| Task | Accuracy | Mean target margin | Mean target prob | Mean target rank |
|---|---:|---:|---:|---:|
| gsm8k | 0.167 | -10.046 | 0.000 | 169.50 |
| mmlu | 0.317 | -14.484 | 0.000 | 709.77 |
| strategyqa | 0.500 | -11.035 | 0.000 | 576.63 |

## Subject summary

| Subject | Accuracy | Mean target margin | Mean target prob |
|---|---:|---:|---:|
| abstract_algebra | 0.500 | -15.995 | 0.000 |
| college_mathematics | 0.250 | -14.328 | 0.000 |
| formal_logic | 0.167 | -14.896 | 0.000 |
| gsm8k | 0.167 | -10.046 | 0.000 |
| high_school_mathematics | 0.083 | -14.294 | 0.000 |
| logical_fallacies | 0.583 | -12.909 | 0.000 |
| strategyqa | 0.500 | -11.035 | 0.000 |

## Interpretation

- If CKA stays high while subspace overlap drops, tasks share broad features but occupy different effective subspaces.
- If centroid trajectories separate by layer, the model is routing tasks into different representational regions.
- If the final-layer manifold clusters by task more strongly than early layers, task specialization is emerging late.
- If principal-direction drift is small, the model is not strongly reshaping geometry even when outputs differ.
- This supports the story that task performance differences may come from representational routing rather than hard gradient conflict.