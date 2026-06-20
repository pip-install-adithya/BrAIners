# Phi-3 residual stream analysis — HGRPO multicheckpoint run

This chapter is the training-trajectory counterpart to the SFT TLens chapter.  
Instead of comparing only the base model and the final checkpoint, it tracks how the residual stream changes across the HGRPO progression.

## Main question

How does the model evolve across checkpoints, and does the late-layer routing improve steadily or simply shift in a different direction?

## What this archive adds

The checkpoint view is valuable because it shows dynamics rather than just endpoints:
- base checkpoint,
- checkpoint-150,
- checkpoint-200,
- checkpoint-250,
- final_model.

This makes the training story more interpretable:
- some layers move early,
- some answer routes become more visible later,
- and the model’s behavior can change without producing a clean accuracy breakthrough.

## How to read the plots

The most important plot is the accuracy progression figure.  
It should be read alongside the checkpoint dashboards and sequence-dynamics figures. Together, they show whether the model is:
- converging,
- over-committing,
- flattening into a single route,
- or changing the answer path without truly improving robustness.

## Mechanistic interpretation

The HGRPO run is useful because it confirms a key theme from the earlier experiments:
optimizing for reward alone does not guarantee better final reasoning behavior.

In the checkpoint dashboards, what often changes most visibly is:
- the confidence profile,
- the output structure,
- and the late-stage residual routing.

That is interesting, but not automatically enough to outperform the strong SFT model on all benchmarks.

## Report-level takeaway

This archive should be presented as a **useful mechanistic progression**, not as the final solution. It is evidence that the model is highly steerable, but the steerability does not always translate into a clean benchmark win.

That is exactly why the project’s final story stays honest:
- SFT is the reliable champion,
- HGRPO is the training-trajectory proof that the model can be moved,
- and RRPO hard-mining is the most promising next-step challenger.

## Phi-3 Multi-Checkpoint Residual Stream Dynamics (HGRPO)

### Global Training Progression

| Training Iteration vs. Task Accuracy Progression |
| :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/accuracy_progression.png" width="85%" alt="Accuracy Progression Across Checkpoints"> |

---

### 1. Base Model Phase Dashboards

#### GSM8K Latent Streams
| Sample 0 Base Dashboard |
| :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/base/gsm8k_0_dashboard.png" width="85%" alt="GSM8K Sample 0 Base Dashboard"> |

| Sample 1 Base Dashboard |
| :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/base/gsm8k_1_dashboard.png" width="85%" alt="GSM8K Sample 1 Base Dashboard"> |

#### StrategyQA Latent Streams
| Sample 0 Base Dashboard |
| :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/base/strategyqa_0_dashboard.png" width="85%" alt="StrategyQA Sample 0 Base Dashboard"> |

| Sample 1 Base Dashboard |
| :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/base/strategyqa_1_dashboard.png" width="85%" alt="StrategyQA Sample 1 Base Dashboard"> |

---

### 2. Checkpoint-150 Mid-Training Dashboards & Layerwise Comparisons

#### Internal Representation Dashboards
| GSM8K Sample 0 Dashboard | StrategyQA Sample 0 Dashboard |
| :---: | :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/checkpoint-150/gsm8k_0_dashboard.png" width="100%" alt="GSM8K Sample 0 Checkpoint 150 Dashboard"> | <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/checkpoint-150/strategyqa_0_dashboard.png" width="100%" alt="StrategyQA Sample 0 Checkpoint 150 Dashboard"> |

| GSM8K Sample 1 Dashboard | StrategyQA Sample 1 Dashboard |
| :---: | :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/checkpoint-150/gsm8k_1_dashboard.png" width="100%" alt="GSM8K Sample 1 Checkpoint 150 Dashboard"> | <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/checkpoint-150/strategyqa_1_dashboard.png" width="100%" alt="StrategyQA Sample 1 Checkpoint 150 Dashboard"> |

#### Checkpoint-150 Attribution & Dynamics Projections
| GSM8K Sample 0 Layerwise Comparison | GSM8K Sample 0 Sequence Dynamics |
| :---: | :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/gsm8k_0_comparison_checkpoint-150.png" width="100%" alt="GSM8K Sample 0 Comparison Checkpoint 150"> | <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/gsm8k_0_sequence_dynamics_checkpoint-150.png" width="100%" alt="GSM8K Sample 0 Sequence Dynamics Checkpoint 150"> |

| GSM8K Sample 1 Layerwise Comparison | GSM8K Sample 1 Sequence Dynamics |
| :---: | :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/gsm8k_1_comparison_checkpoint-150.png" width="100%" alt="GSM8K Sample 1 Comparison Checkpoint 150"> | <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/gsm8k_1_sequence_dynamics_checkpoint-150.png" width="100%" alt="GSM8K Sample 1 Sequence Dynamics Checkpoint 150"> |

| StrategyQA Sample 0 Layerwise Comparison | StrategyQA Sample 0 Sequence Dynamics |
| :---: | :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/strategyqa_0_comparison_checkpoint-150.png" width="100%" alt="StrategyQA Sample 0 Comparison Checkpoint 150"> | <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/strategyqa_0_sequence_dynamics_checkpoint-150.png" width="100%" alt="StrategyQA Sample 0 Sequence Dynamics Checkpoint 150"> |

| StrategyQA Sample 1 Layerwise Comparison | StrategyQA Sample 1 Sequence Dynamics |
| :---: | :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/strategyqa_1_comparison_checkpoint-150.png" width="100%" alt="StrategyQA Sample 1 Comparison Checkpoint 150"> | <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/strategyqa_1_sequence_dynamics_checkpoint-150.png" width="100%" alt="StrategyQA Sample 1 Sequence Dynamics Checkpoint 150"> |

---

### 3. Checkpoint-200 Mid-Training Dashboards & Layerwise Comparisons

#### Internal Representation Dashboards
| GSM8K Sample 0 Dashboard | StrategyQA Sample 0 Dashboard |
| :---: | :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/checkpoint-200/gsm8k_0_dashboard.png" width="100%" alt="GSM8K Sample 0 Checkpoint 200 Dashboard"> | <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/checkpoint-200/strategyqa_0_dashboard.png" width="100%" alt="StrategyQA Sample 0 Checkpoint 200 Dashboard"> |

| GSM8K Sample 1 Dashboard | StrategyQA Sample 1 Dashboard |
| :---: | :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/checkpoint-200/gsm8k_1_dashboard.png" width="100%" alt="GSM8K Sample 1 Checkpoint 200 Dashboard"> | <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/checkpoint-200/strategyqa_1_dashboard.png" width="100%" alt="StrategyQA Sample 1 Checkpoint 200 Dashboard"> |

#### Checkpoint-200 Attribution & Dynamics Projections
| GSM8K Sample 0 Layerwise Comparison | GSM8K Sample 0 Sequence Dynamics |
| :---: | :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/gsm8k_0_comparison_checkpoint-200.png" width="100%" alt="GSM8K Sample 0 Comparison Checkpoint 200"> | <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/gsm8k_0_sequence_dynamics_checkpoint-200.png" width="100%" alt="GSM8K Sample 0 Sequence Dynamics Checkpoint 200"> |

| GSM8K Sample 1 Layerwise Comparison | GSM8K Sample 1 Sequence Dynamics |
| :---: | :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/gsm8k_1_comparison_checkpoint-200.png" width="100%" alt="GSM8K Sample 1 Comparison Checkpoint 200"> | <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/gsm8k_1_sequence_dynamics_checkpoint-200.png" width="100%" alt="GSM8K Sample 1 Sequence Dynamics Checkpoint 200"> |

| StrategyQA Sample 0 Layerwise Comparison | StrategyQA Sample 0 Sequence Dynamics |
| :---: | :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/strategyqa_0_comparison_checkpoint-200.png" width="100%" alt="StrategyQA Sample 0 Comparison Checkpoint 200"> | <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/strategyqa_0_sequence_dynamics_checkpoint-200.png" width="100%" alt="StrategyQA Sample 0 Sequence Dynamics Checkpoint 200"> |

| StrategyQA Sample 1 Layerwise Comparison | StrategyQA Sample 1 Sequence Dynamics |
| :---: | :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/strategyqa_1_comparison_checkpoint-200.png" width="100%" alt="StrategyQA Sample 1 Comparison Checkpoint 200"> | <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/strategyqa_1_sequence_dynamics_checkpoint-200.png" width="100%" alt="StrategyQA Sample 1 Sequence Dynamics Checkpoint 200"> |

---

### 4. Checkpoint-250 Mid-Training Dashboards & Layerwise Comparisons

#### Internal Representation Dashboards
| GSM8K Sample 0 Dashboard | StrategyQA Sample 0 Dashboard |
| :---: | :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/checkpoint-250/gsm8k_0_dashboard.png" width="100%" alt="GSM8K Sample 0 Checkpoint 250 Dashboard"> | <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/checkpoint-250/strategyqa_0_dashboard.png" width="100%" alt="StrategyQA Sample 0 Checkpoint 250 Dashboard"> |

| GSM8K Sample 1 Dashboard | StrategyQA Sample 1 Dashboard |
| :---: | :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/checkpoint-250/gsm8k_1_dashboard.png" width="100%" alt="GSM8K Sample 1 Checkpoint 250 Dashboard"> | <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/checkpoint-250/strategyqa_1_dashboard.png" width="100%" alt="StrategyQA Sample 1 Checkpoint 250 Dashboard"> |

#### Checkpoint-250 Attribution & Dynamics Projections
| GSM8K Sample 0 Layerwise Comparison | GSM8K Sample 0 Sequence Dynamics |
| :---: | :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/gsm8k_0_comparison_checkpoint-250.png" width="100%" alt="GSM8K Sample 0 Comparison Checkpoint 250"> | <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/gsm8k_0_sequence_dynamics_checkpoint-250.png" width="100%" alt="GSM8K Sample 0 Sequence Dynamics Checkpoint 250"> |

| GSM8K Sample 1 Layerwise Comparison | GSM8K Sample 1 Sequence Dynamics |
| :---: | :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/gsm8k_1_comparison_checkpoint-250.png" width="100%" alt="GSM8K Sample 1 Comparison Checkpoint 250"> | <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/gsm8k_1_sequence_dynamics_checkpoint-250.png" width="100%" alt="GSM8K Sample 1 Sequence Dynamics Checkpoint 250"> |

| StrategyQA Sample 0 Layerwise Comparison | StrategyQA Sample 0 Sequence Dynamics |
| :---: | :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/strategyqa_0_comparison_checkpoint-250.png" width="100%" alt="StrategyQA Sample 0 Comparison Checkpoint 250"> | <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/strategyqa_0_sequence_dynamics_checkpoint-250.png" width="100%" alt="StrategyQA Sample 0 Sequence Dynamics Checkpoint 250"> |

| StrategyQA Sample 1 Layerwise Comparison | StrategyQA Sample 1 Sequence Dynamics |
| :---: | :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/strategyqa_1_comparison_checkpoint-250.png" width="100%" alt="StrategyQA Sample 1 Comparison Checkpoint 250"> | <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/strategyqa_1_sequence_dynamics_checkpoint-250.png" width="100%" alt="StrategyQA Sample 1 Sequence Dynamics Checkpoint 250"> |

---

### 5. Final Convergence Model Dashboards & Layerwise Comparisons

#### Internal Representation Dashboards
| GSM8K Sample 0 Dashboard | StrategyQA Sample 0 Dashboard |
| :---: | :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/final_model/gsm8k_0_dashboard.png" width="100%" alt="GSM8K Sample 0 Final Model Dashboard"> | <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/final_model/strategyqa_0_dashboard.png" width="100%" alt="StrategyQA Sample 0 Final Model Dashboard"> |

| GSM8K Sample 1 Dashboard | StrategyQA Sample 1 Dashboard |
| :---: | :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/final_model/gsm8k_1_dashboard.png" width="100%" alt="GSM8K Sample 1 Final Model Dashboard"> | <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/final_model/strategyqa_1_dashboard.png" width="100%" alt="StrategyQA Sample 1 Final Model Dashboard"> |

#### Final Converged Attribution & Dynamics Projections
| GSM8K Sample 0 Layerwise Comparison | GSM8K Sample 0 Sequence Dynamics |
| :---: | :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/gsm8k_0_comparison_final_model.png" width="100%" alt="GSM8K Sample 0 Comparison Final Model"> | <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/gsm8k_0_sequence_dynamics_final_model.png" width="100%" alt="GSM8K Sample 0 Sequence Dynamics Final Model"> |

| GSM8K Sample 1 Layerwise Comparison | GSM8K Sample 1 Sequence Dynamics |
| :---: | :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/gsm8k_1_comparison_final_model.png" width="100%" alt="GSM8K Sample 1 Comparison Final Model"> | <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/gsm8k_1_sequence_dynamics_final_model.png" width="100%" alt="GSM8K Sample 1 Sequence Dynamics Final Model"> |

| StrategyQA Sample 0 Layerwise Comparison | StrategyQA Sample 0 Sequence Dynamics |
| :---: | :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/strategyqa_0_comparison_final_model.png" width="100%" alt="StrategyQA Sample 0 Comparison Final Model"> | <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/strategyqa_0_sequence_dynamics_final_model.png" width="100%" alt="StrategyQA Sample 0 Sequence Dynamics Final Model"> |

| StrategyQA Sample 1 Layerwise Comparison | StrategyQA Sample 1 Sequence Dynamics |
| :---: | :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/strategyqa_1_comparison_final_model.png" width="100%" alt="StrategyQA Sample 1 Comparison Final Model"> | <img src="../../src/t_lens/phi3_residual_stream_deep_insights_hgrpo/phi3_residual_stream_deep_insights/plots/comparisons/strategyqa_1_sequence_dynamics_final_model.png" width="100%" alt="StrategyQA Sample 1 Sequence Dynamics Final Model"> |

The sample IDs visible in the TLens archive are:
- `gsm8k_0`
- `gsm8k_1`
- `strategyqa_0`
- `strategyqa_1`

## Closing line

This chapter is the bridge between training and mechanistic diagnosis: it shows what the model changed into, not only whether it improved.