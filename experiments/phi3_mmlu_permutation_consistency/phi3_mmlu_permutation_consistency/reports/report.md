# MMLU permutation-consistency experiment

- Model: `microsoft/phi-3-mini-4k-instruct`
- Subjects: abstract_algebra, college_mathematics, logical_fallacies, formal_logic, high_school_mathematics
- Questions per subject: 8
- Permutations per question: 12
- Delimiter prompt: True
- Plain-prompt baseline: False

## Overall results

| Prompt variant | Original acc | Permuted acc | Consistency | Content stability | Raw bias |
|---|---:|---:|---:|---:|---:|
| anchored | 0.375 | 0.419 | 0.594 | 0.594 | 0.408 |

## Subject breakdown

| Prompt variant | Subject | Original acc | Permuted acc | Consistency | Content stability | Raw bias |
|---|---|---:|---:|---:|---:|---:|
| anchored | abstract_algebra | 0.250 | 0.385 | 0.552 | 0.552 | 0.500 |
| anchored | college_mathematics | 0.125 | 0.188 | 0.469 | 0.469 | 0.427 |
| anchored | formal_logic | 0.250 | 0.312 | 0.635 | 0.635 | 0.417 |
| anchored | high_school_mathematics | 0.250 | 0.302 | 0.406 | 0.406 | 0.229 |
| anchored | logical_fallacies | 1.000 | 0.906 | 0.906 | 0.906 | 0.469 |

## Interpretation hints

- High raw letter bias with lower canonical consistency suggests answer-position heuristics.
- High content stability with high permuted accuracy suggests genuine option-content reasoning.
- Low consistency but moderate original accuracy suggests order sensitivity.
- The confusion matrix shows whether certain gold letters are systematically favored.
- Positional Bias Heatmap (magma) reveals if your model falls back to picking 'C' when unsure, regardless of contents.