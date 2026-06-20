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

## Phi-3 MMLU Permutation Lattice Experiment Results

### Matrix Analytics & Subject Heatmaps

| Style Metrics | Subject Distributions |
| :---: | :---: |
| <img src="../../src/advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/style_metric_heatmap.png" height="220" alt="Style Metric Heatmap"> | <img src="../../src/advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/subject_metric_heatmap.png" height="220" alt="Subject Metric Heatmap"> |
| | <img src="../../src/advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/subject_ridgeline.png" height="220" alt="Subject Ridgeline"> |

---

### Permutation Invariance & Information Entropy

| Consistency Metrics | Metric State Space Overlaps |
| :---: | :---: |
| <img src="../../src/advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/question_permutation_entropy_hist.png" height="220" alt="Question Permutation Entropy Histogram"> | <img src="../../src/advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/stability_vs_accuracy_scatter.png" height="220" alt="Stability vs Accuracy Scatter"> |
| <img src="../../src/advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/question_stability_scores.png" height="220" alt="Question Stability Scores"> | <img src="../../src/advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/entropy_vs_invariance_hexbin.png" height="220" alt="Entropy vs Invariance Hexbin"> |

---

### Subject-Wise Specific Lattice Dimensions

#### Mathematics and Algebra Domains
| Topography 3D Surface | Hierarchical Clustering |
| :---: | :---: |
| <img src="../../src/advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/abstract_algebra_dla_surface_3d.png" height="220" alt="Abstract Algebra DLA Surface 3D"> | <img src="../../src/advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/abstract_algebra_dla_dendrogram.png" height="220" alt="Abstract Algebra DLA Dendrogram"> |
| <img src="../../src/advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/college_mathematics_dla_surface_3d.png" height="220" alt="College Mathematics DLA Surface 3D"> | <img src="../../src/advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/college_mathematics_dla_dendrogram.png" height="220" alt="College Mathematics DLA Dendrogram"> |
| <img src="../../src/advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/high_school_mathematics_dla_surface_3d.png" height="220" alt="High School Mathematics DLA Surface 3D"> | <img src="../../src/advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/high_school_mathematics_dla_dendrogram.png" height="220" alt="High School Mathematics DLA Dendrogram"> |

#### Logic and Reason Fallacies
| Topography 3D Surface | Hierarchical Clustering |
| :---: | :---: |
| <img src="../../src/advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/formal_logic_dla_surface_3d.png" height="220" alt="Formal Logic DLA Surface 3D"> | <img src="../../src/advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/formal_logic_dla_dendrogram.png" height="220" alt="Formal Logic DLA Dendrogram"> |
| <img src="../../src/advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/logical_fallacies_dla_surface_3d.png" height="220" alt="Logical Fallacies DLA Surface 3D"> | <img src="../../src/advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/logical_fallacies_dla_dendrogram.png" height="220" alt="Logical Fallacies DLA Dendrogram"> |

---

### Comprehensive Style Summary Dashboard

| Overview Control Dashboard |
| :---: |
| <img src="../../src/advanced_experiments/phi3_mmlu_permutation_lattice/mmlu_permutation_lattice_atlas/plots/style_summary_dashboard.png" width="85%" alt="Style Summary Dashboard"> |

## Conclusion

Permutation invariance is a real property, not an aesthetic detail.  
The model needs to be trained and evaluated in a way that respects answer-slot fragility.