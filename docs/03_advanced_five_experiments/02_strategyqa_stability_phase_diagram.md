# StrategyQA stability phase diagram

This experiment treats StrategyQA as a dynamical system rather than a static classification task.

## Core question

Is the model sitting inside a stable yes/no basin, or is it hovering near a fragile boundary where tiny prompt changes cause flips?

## What is measured

The analysis tracks:
- confidence,
- commitment,
- calibration,
- transition entropy,
- pass-1 / pass-2 behavior,
- and phase portraits of the decision process.

## Main findings

The baseline plain variant shows:
- raw pass-1 accuracy around 0.45
- raw pass-2 accuracy around 0.425
- calibrated pass-1 accuracy around 0.583
- calibrated pass-2 accuracy around 0.592

That tells us the model contains useful latent signal, but that signal is not always emitted cleanly.

The important story is that:
- text drift and confidence drift are not the same thing,
- some examples are stable and some are flip-prone,
- and prompt changes can move the question across a decision boundary.

## Why it matters

This experiment directly supports:
- threshold calibration,
- commitment rewards,
- anti-bias penalties,
- and self-correction routing.

It also explains why StrategyQA is not just a “knowledge benchmark.”  
It is a decision-process benchmark.

## Phi-3 StrategyQA Stability Phase Diagram Experiment Results

### Latent Space Dynamics and State Trajectories

| Phase Space Portraits | Attractors & Transitions |
| :---: | :---: |
| <img src="../../src/advanced_experiments/phi3_stratqa_stability_phase_diagram/strategyqa_stability_phase_diagram/plots/phase_portrait_baseline.png" height="250" alt="Phase Portrait Baseline"> | <img src="../../src/advanced_experiments/phi3_stratqa_stability_phase_diagram/strategyqa_stability_phase_diagram/plots/transition_heatmap_baseline.png" height="250" alt="Transition Heatmap Baseline"> |
| <img src="../../src/advanced_experiments/phi3_stratqa_stability_phase_diagram/strategyqa_stability_phase_diagram/plots/phase_space_3d_trajectories.png" height="250" alt="Phase Space 3D Trajectories"> | <img src="../../src/advanced_experiments/phi3_stratqa_stability_phase_diagram/strategyqa_stability_phase_diagram/plots/transition_entropy_hist.png" height="250" alt="Transition Entropy Histogram"> |

---

### Stability & Accuracy Breakdown

| Stability Distributions | Calibration & Diagnostics |
| :---: | :---: |
| <img src="../../src/advanced_experiments/phi3_stratqa_stability_phase_diagram/strategyqa_stability_phase_diagram/plots/question_stability_scores.png" height="220" alt="Question Stability Scores"> | <img src="../../src/advanced_experiments/phi3_stratqa_stability_phase_diagram/strategyqa_stability_phase_diagram/plots/reliability_pass1_baseline.png" height="220" alt="Reliability Pass 1 Baseline"> |
| <img src="../../src/advanced_experiments/phi3_stratqa_stability_phase_diagram/strategyqa_stability_phase_diagram/plots/stability_vs_pass2_accuracy.png" height="220" alt="Stability vs Pass 2 Accuracy"> | <img src="../../src/advanced_experiments/phi3_stratqa_stability_phase_diagram/strategyqa_stability_phase_diagram/plots/reliability_pass2_baseline.png" height="220" alt="Reliability Pass 2 Baseline"> |

---

### Log-Odds Distributions and Bifurcations

| Sequential Distributions | Global Bifurcation Maps |
| :---: | :---: |
| <img src="../../src/advanced_experiments/phi3_stratqa_stability_phase_diagram/strategyqa_stability_phase_diagram/plots/pass1_logodds_hist.png" height="220" alt="Pass 1 Log-Odds Histogram"> | <img src="../../src/advanced_experiments/phi3_stratqa_stability_phase_diagram/strategyqa_stability_phase_diagram/plots/bifurcation_hexbin_all_variants.png" height="220" alt="Bifurcation Hexbin All Variants"> |
| <img src="../../src/advanced_experiments/phi3_stratqa_stability_phase_diagram/strategyqa_stability_phase_diagram/plots/pass2_logodds_hist.png" height="220" alt="Pass 2 Log-Odds Histogram"> | <img src="../../src/advanced_experiments/phi3_stratqa_stability_phase_diagram/strategyqa_stability_phase_diagram/plots/variant_logodds_ridgeplot.png" height="220" alt="Variant Log-Odds Ridgeplot"> |

---

### Multi-Variant Fingerprints and Dashboards

| Cross-Metric Heatmaps | Radar Fingerprints |
| :---: | :---: |
| <img src="../../src/advanced_experiments/phi3_stratqa_stability_phase_diagram/strategyqa_stability_phase_diagram/plots/variant_metric_map.png" height="220" alt="Variant Metric Map"> | <img src="../../src/advanced_experiments/phi3_stratqa_stability_phase_diagram/strategyqa_stability_phase_diagram/plots/variant_radar_fingerprint.png" height="220" alt="Variant Radar Fingerprint"> |

| Comprehensive Experiment Overview |
| :---: |
| <img src="../../src/advanced_experiments/phi3_stratqa_stability_phase_diagram/strategyqa_stability_phase_diagram/plots/overall_variant_dashboard.png" width="85%" alt="Overall Variant Dashboard"> |

## Conclusion

StrategyQA behaves like a stability basin problem.  
That is why calibration and commitment rewards are more useful than raw free-form generation rewards.