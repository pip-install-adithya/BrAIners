# StrategyQA self-correction basin atlas

This is the expanded self-correction experiment.  
It asks when a second pass helps, when it harms, and when it does nothing.

## Experimental setup

- Validation samples: 120
- Test samples: 120
- Prompt variants:
  - plain
  - anchored
  - anchored_reason
  - anchored_xml
  - anchored_selfcheck
  - answer_first
  - verbose
- Baseline variant: plain
- Deterministic decoding: yes

## Main findings

The baseline plain variant shows:
- pass-1 raw accuracy = 0.450
- pass-2 raw accuracy = 0.425
- pass-1 calibrated accuracy = 0.583
- pass-2 calibrated accuracy = 0.592
- improvement rate = 0.125
- regression rate = 0.150
- transition entropy = 1.831
- mean Q stability = 0.642
- mean Q drift = 0.303

The variant table shows that:
- anchored_reason has strong pass-1 accuracy,
- anchored_xml and anchored_selfcheck can improve some cases,
- answer_first is fragile and regresses often,
- verbose tends to increase drift.

The basin class counts show that the model is not uniformly stable:
- moderately stable basin: 53
- stable correct basin: 33
- uncertain basin: 17
- stable but diverse basin: 10
- flip-prone basin: 7

## Why it matters

Self-correction is not a free improvement layer.  
It is a conditional transition mechanism.

The basin atlas is valuable because it separates:
- genuinely recoverable mistakes,
- from already-correct answers that become unstable under review.

That directly motivates:
- verifier-guided second passes,
- self-critique only on selected cases,
- and conditional routing rather than universal self-correction.

## Figures to embed

- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/overall_dashboard.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/variant_metrics_dashboard.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/variant_metric_heatmap.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/basin_atlas_baseline.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/basin_atlas_all_variants.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/basin_class_counts.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/phase_portrait_baseline.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/trajectory_field_baseline.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/trajectory_field_all_variants.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/transition_heatmap_baseline.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/strip_transitions_baseline.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/strip_transitions_all_variants.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/reliability_plain_pass1.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/reliability_plain_pass2.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/reliability_anchored_reason_pass1.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/reliability_anchored_reason_pass2.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/question_stability_scores.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/question_transition_entropy_hist.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/question_response_drift_hist.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/response_drift_baseline.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/response_drift_all_variants.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/entropy_vs_improvement.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/drift_vs_delta_logodds.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/stability_vs_pass2_accuracy.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/self_correction_waterfall.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/glyph_atlas_all.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/representative_trajectories_all.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/bifurcation_all_variants.png`
- `../advanced_experiments/phi3_stratqa_self_correction_basin_atlas/strategyqa_self_correction_basin_atlas/plots/accuracy_comparison_grouped.png`

## Conclusion

Self-correction is useful only in the right basin.  
This experiment justifies selective routing and verifier-guided second passes.