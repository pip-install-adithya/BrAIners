# Task interference / gradient conflict experiment

This experiment asks whether GSM8K, StrategyQA, and MMLU share the same internal update geometry or whether they occupy different spaces.

## Experimental setup

- Model: `microsoft/phi-3-mini-4k-instruct`
- Tasks: gsm8k, strategyqa, mmlu
- GSM8K samples: 5
- StrategyQA samples: 5
- MMLU samples per subject: 3
- MMLU subjects:
  - abstract_algebra
  - college_mathematics
  - logical_fallacies
- Gradient layers: 26–31
- Representation layers: 0–9 and deeper summaries

## Main results

### Evaluation summary

| Task | Greedy accuracy | Mean loss | Std loss | Mean prompt tokens | Mean completion tokens |
|---|---:|---:|---:|---:|---:|
| gsm8k | 0.200 | 0.385 | 0.171 | 86.6 | 64.4 |
| strategyqa | 0.400 | 9.286 | 0.899 | 22.6 | 16.6 |
| mmlu | 0.556 | 7.124 | 4.166 | 88.7 | 16.2 |

### Gradient conflict summary

The pairwise gradient-cosine table shows no strong direct negative-gradient signal in the sampled setup, but that does not mean the tasks are identical.

### Representation overlap summary

| Task A | Task B | Mean subspace overlap | Mean centroid cosine | Mean CKA |
|---|---|---:|---:|---:|
| gsm8k | strategyqa | 0.1254 | 0.8495 | 0.4704 |
| gsm8k | mmlu | 0.1746 | 0.9515 | 0.5197 |
| strategyqa | mmlu | 0.2156 | 0.9471 | 0.7425 |

## Interpretation

The strongest result here is geometric, not gradient-based.

The tasks are not fully conflicting in the naive sense.  
Instead:
- they overlap in some broad representational directions,
- but they still occupy different effective subspaces,
- which suggests that routing and task geometry matter more than a single “negative gradient” story.

This strongly supports:
- adapter-based specialization,
- routed reward structures,
- and task-aware intervention design.

It also explains why the same training recipe can help one task and leave another unchanged.

## Figures to embed

- `../experiments/phi3_task_inference_gradient_conflict/phi3_task_interference/plots/mmlu_accuracy.png`
- `../experiments/phi3_task_inference_gradient_conflict/phi3_task_interference/plots/mmlu_loss.png`
- `../experiments/phi3_task_inference_gradient_conflict/phi3_task_interference/plots/mmlu_loss_hist.png`
- `../experiments/phi3_task_inference_gradient_conflict/phi3_task_interference/plots/grad_norm_mmlu.png`
- `../experiments/phi3_task_inference_gradient_conflict/phi3_task_interference/plots/gradient_cosine_gsm8k_vs_mmlu.png`
- `../experiments/phi3_task_inference_gradient_conflict/phi3_task_interference/plots/gradient_dot_gsm8k_vs_mmlu.png`
- `../experiments/phi3_task_inference_gradient_conflict/phi3_task_interference/plots/gradient_cosine_strategyqa_vs_mmlu.png`
- `../experiments/phi3_task_inference_gradient_conflict/phi3_task_interference/plots/gradient_dot_strategyqa_vs_mmlu.png`
- `../experiments/phi3_task_inference_gradient_conflict/phi3_task_interference/plots/rep_cka_gsm8k_vs_mmlu.png`
- `../experiments/phi3_task_inference_gradient_conflict/phi3_task_interference/plots/rep_cka_strategyqa_vs_mmlu.png`
- `../experiments/phi3_task_inference_gradient_conflict/phi3_task_interference/plots/rep_overlap_gsm8k_vs_mmlu.png`
- `../experiments/phi3_task_inference_gradient_conflict/phi3_task_interference/plots/rep_overlap_strategyqa_vs_mmlu.png`
- `../experiments/phi3_task_inference_gradient_conflict/phi3_task_interference/plots/mmlu_delimiter_vs_plain_accuracy.png`

## Conclusion

Task interference is present, but it is mostly geometric rather than obviously destructive in the sampled gradients.  
That supports routing, adapters, and task-specific reward design.