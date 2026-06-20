# MMLU permutation lattice

This is the densest answer-order experiment in the project.

## Core question

Does the model keep selecting the same underlying answer content when the answer choices are permuted?

## Experimental setup

- Subjects:
  - abstract_algebra
  - college_mathematics
  - logical_fallacies
  - formal_logic
  - high_school_mathematics
- Questions per subject: 8
- Permutations per question: 12

## Main findings

The anchored variant shows:
- original accuracy = 0.375
- permuted accuracy = 0.419
- consistency = 0.594
- content stability = 0.594
- raw bias = 0.408

Subject-level results show that:
- logical_fallacies is strong and relatively stable,
- high_school_mathematics is more fragile,
- the math-heavy subjects are the most sensitive to permutation and content mapping.

## Why it matters

This experiment makes the answer-position issue measurable.

If the model is stable under permutation, it is reasoning over the content.  
If it shifts with the option order, it is using a shortcut.

The lattice representation is useful because it exposes:
- answer-slot bias,
- content stability,
- permutation entropy,
- subject-specific fragility,
- and the relationship between raw bias and actual correctness.

This is one of the strongest justifications for answer-order-aware reward shaping.

## Figures to embed

- `../advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/style_summary_dashboard.png`
- `../advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/raw_letter_distribution.png`
- `../advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/canonical_letter_distribution.png`
- `../advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/positional_bias_heatmap.png`
- `../advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/confusion_matrix_heatmap.png`
- `../advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/consistency_histogram.png`
- `../advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/stability_vs_accuracy_scatter.png`
- `../advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/consistency_vs_accuracy_hexbin.png`
- `../advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/question_permutation_entropy_hist.png`
- `../advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/question_stability_scores.png`
- `../advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/subject_metric_heatmap.png`
- `../advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/subject_ridgeline.png`
- `../advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/subject_original_accuracy.png`
- `../advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/subject_permuted_accuracy.png`
- `../advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/subject_consistency_score.png`
- `../advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/subject_content_stability.png`
- `../advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/subject_raw_bias_fraction.png`
- `../advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/entropy_vs_invariance_hexbin.png`
- `../advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/radar_chart_anchored.png`

## Conclusion

Permutation invariance is a real property, not an aesthetic detail.  
The model needs to be trained and evaluated in a way that respects answer-slot fragility.