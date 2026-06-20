# Task geometry atlas

This is the geometry-first experiment.  
It asks how GSM8K, StrategyQA, and MMLU occupy representation space across depth.

## Experimental setup

- Samples:
  - GSM8K = 30
  - StrategyQA = 30
  - MMLU per subject = 12
- Subjects:
  - abstract_algebra
  - college_mathematics
  - logical_fallacies
  - formal_logic
  - high_school_mathematics

## Main findings

| Task | Accuracy | Mean target margin | Mean target prob | Mean target rank |
|---|---:|---:|---:|---:|
| gsm8k | 0.167 | -10.046 | 0.000 | 169.50 |
| mmlu | 0.317 | -14.484 | 0.000 | 709.77 |
| strategyqa | 0.500 | -11.035 | 0.000 | 576.63 |

The subject-level table shows:
- logical_fallacies is strongest,
- high_school_mathematics is weakest,
- the math-heavy subjects are consistently harder.

## Interpretation

This experiment shows that the model does not treat all tasks as the same internal problem.

The representation space contains:
- task-specific centroids,
- subspace overlap that drops with depth,
- late-layer clustering by task,
- and principal-direction drift that is not large enough to imply total restructuring.

That supports a routing-based view:
- different tasks occupy different regions,
- and the model’s final decision behavior depends on where the representation ends up.

This is a central justification for:
- mixture-of-adapters ideas,
- task routing,
- and diagnostic-routed reward design.

## Figures to embed

- `../advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/task_geometry_atlas_dashboard.png`
- `../advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/layerwise_geometry_summary.png`
- `../advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/accuracy_and_margin_dashboard.png`
- `../advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/task_centroid_trajectories.png`
- `../advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/task_centroid_trajectory_pca.png`
- `../advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/task_manifold_3d_final.png`
- `../advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/task_manifold_final_layer.png`
- `../advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/final_layer_embedding_cloud.png`
- `../advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/final_layer_similarity_ridges.png`
- `../advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/final_centroid_separation_heatmap.png`
- `../advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/cka_layers_dashboard.png`
- `../advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/cka_pairwise_layer_heatmap.png`
- `../advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/subspace_overlap_ribbon.png`
- `../advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/pairwise_centroid_distance_dashboard.png`
- `../advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/principal_direction_drift_dashboard.png`
- `../advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/sample_feature_correlation.png`
- `../advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/task_taxonomy_dendrogram.png`
- `../advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/violin_target_margin.png`
- `../advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/violin_target_prob.png`

## Conclusion

Task geometry matters.  
The model’s behavior is partly a routing problem over representational space, not only a prediction problem.