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

## Phi-3 Task Geometry Atlas Experiment Results

### High-Dimensional Manifolds & Trajectory Dynamics

#### Latent Representation Landscapes
| Geometric Task Manifold (3D Final Projection) |
| :---: |
| <img src="../../src/advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/task_manifold_3d_final.png" width="85%" alt="Task Manifold 3D Final"> |

#### Hidden Layer Evolution Streams
| Layerwise Task Centroid Trajectories |
| :---: |
| <img src="../../src/advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/task_centroid_trajectories.png" width="85%" alt="Task Centroid Trajectories"> |

| Principal Component Projections | Final Processing Layer State |
| :---: | :---: |
| <img src="../../src/advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/task_centroid_trajectory_pca.png" height="220" alt="Task Centroid Trajectory PCA"> | <img src="../../src/advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/task_manifold_final_layer.png" height="220" alt="Task Manifold Final Layer"> |

---

### Layerwise Representation & Centroid Separation

#### Metric Extraction Landscapes
| Centroid Spatial Distance Dashboard |
| :---: |
| <img src="../../src/advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/pairwise_centroid_distance_dashboard.png" width="85%" alt="Pairwise Centroid Distance Dashboard"> |

| Convergent Discrepancy Heatmaps | Target Subspace Topography |
| :---: | :---: |
| <img src="../../src/advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/final_centroid_separation_heatmap.png" height="220" alt="Final Centroid Separation Heatmap"> | <img src="../../src/advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/final_layer_similarity_ridges.png" height="220" alt="Final Layer Similarity Ridges"> |
| <img src="../../src/advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/subspace_overlap_ribbon.png" height="220" alt="Subspace Overlap Ribbon"> | <img src="../../src/advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/task_taxonomy_dendrogram.png" height="220" alt="Task Taxonomy Dendrogram"> |

#### High-Density Activation Clouds
| Final Layer Token Embedding Point Cloud |
| :---: |
| <img src="../../src/advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/final_layer_embedding_cloud.png" width="85%" alt="Final Layer Embedding Cloud"> |

---

### Similarity, Representation Alignment & Drift

#### Multi-Layer Representation Tracking
| Canonical Correlation Analysis (CKA) Dashboard |
| :---: |
| <img src="../../src/advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/cka_layers_dashboard.png" width="85%" alt="CKA Layers Dashboard"> |

| Principal Vector Drift Dashboard |
| :---: |
| <img src="../../src/advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/principal_direction_drift_dashboard.png" width="85%" alt="Principal Direction Drift Dashboard"> |

| Internal Alignment Matrices | Cross-Layer Feature Correlations |
| :---: | :---: |
| <img src="../../src/advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/cka_pairwise_layer_heatmap.png" height="220" alt="CKA Pairwise Layer Heatmap"> | <img src="../../src/advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/sample_feature_correlation.png" height="220" alt="Sample Feature Correlation"> |
| <img src="../../src/advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/layerwise_geometry_summary.png" height="220" alt="Layerwise Geometry Summary"> | |

---

### Target Probabilities & Certainty Margins

#### Margin Calibration Diagnostics
| Evaluation Accuracy & Prediction Margin Dashboard |
| :---: |
| <img src="../../src/advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/accuracy_and_margin_dashboard.png" width="85%" alt="Accuracy and Margin Dashboard"> |

| Certainty Index Densities | Target Logit Proximity |
| :---: | :---: |
| <img src="../../src/advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/violin_target_prob.png" height="220" alt="Violin Target Probabilities"> | <img src="../../src/advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/violin_target_margin.png" height="220" alt="Violin Target Margin"> |

---

### Global Geometry Control Panel

#### Comprehensive Atlas Summary
| Overall Task Geometry Control Dashboard |
| :---: |
| <img src="../../src/advanced_experiments/phi3_task_geometry_atlas/task_geometry_atlas/plots/task_geometry_atlas_dashboard.png" width="85%" alt="Task Geometry Atlas Dashboard"> |

## Conclusion

Task geometry matters.  
The model’s behavior is partly a routing problem over representational space, not only a prediction problem.