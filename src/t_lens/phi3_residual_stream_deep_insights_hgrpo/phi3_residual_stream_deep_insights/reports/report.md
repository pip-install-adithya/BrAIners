# Phi-3 Residual Stream Multi-Checkpoint Report

- Base model: `microsoft/phi-3-mini-4k-instruct`
- Checkpoints directory: `/kaggle/input/datasets/adithyal2/phi3-adapterss/hierarchical_steering_grpo_phi3/checkpoints`
- Models analyzed: `base`, `checkpoint-150`, `checkpoint-200`, `checkpoint-250`, `final_model`
- Samples per benchmark: GSM8K=2, StrategyQA=2, MMLU=2

## Global Progression Summary

| model          | task       |   n |   accuracy |   format_rate |   hedge_rate |   avg_len |
|:---------------|:-----------|----:|-----------:|--------------:|-------------:|----------:|
| base           | gsm8k      |   2 |        0.5 |           0.5 |            0 |       103 |
| base           | strategyqa |   2 |        1   |           1   |            0 |         1 |
| checkpoint-150 | gsm8k      |   2 |        0.5 |           0.5 |            0 |       103 |
| checkpoint-150 | strategyqa |   2 |        1   |           1   |            0 |         1 |
| checkpoint-200 | gsm8k      |   2 |        0.5 |           0.5 |            0 |       103 |
| checkpoint-200 | strategyqa |   2 |        1   |           1   |            0 |         1 |
| checkpoint-250 | gsm8k      |   2 |        0.5 |           0.5 |            0 |        95 |
| checkpoint-250 | strategyqa |   2 |        1   |           1   |            0 |         1 |
| final_model    | gsm8k      |   2 |        0.5 |           0.5 |            0 |        95 |
| final_model    | strategyqa |   2 |        1   |           1   |            0 |         1 |

## Notes

- Residual stream representations are visualised for multiple benchmarks.
- Sequence dynamics plot token-by-token processing states in the final layer.
- The code loads only one model at a time to avoid Kaggle OOMs, running through all checkpoints sequentially.
- Comparison dashboards map 'base' vs each fine-tuned checkpoint.
- Verbose timestamps and GPU memory reports are included around expensive steps.