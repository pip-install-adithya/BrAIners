# Phi-3 residual stream report

- Base model: `microsoft/phi-3-mini-4k-instruct`
- SFT source: `/kaggle/input/datasets/adithyaled24b039/phi3-sft-folderr/phi3_sft_lora`
- Samples per benchmark: GSM8K=2, StrategyQA=2, MMLU=2

## Base summary

| task       |   n |   accuracy |   format_rate |   hedge_rate |   avg_len |
|:-----------|----:|-----------:|--------------:|-------------:|----------:|
| gsm8k      |   2 |          0 |             0 |            0 |       256 |
| strategyqa |   2 |          0 |             0 |            0 |       192 |

## SFT summary

| task       |   n |   accuracy |   format_rate |   hedge_rate |   avg_len |
|:-----------|----:|-----------:|--------------:|-------------:|----------:|
| gsm8k      |   2 |          0 |             0 |            0 |     256   |
| strategyqa |   2 |          0 |             0 |            0 |      99.5 |

## Comparison

| task       |   n_base |   accuracy_base |   format_rate_base |   hedge_rate_base |   avg_len_base |   n_sft |   accuracy_sft |   format_rate_sft |   hedge_rate_sft |   avg_len_sft |   delta_accuracy |   delta_format_rate |   delta_hedge_rate |
|:-----------|---------:|----------------:|-------------------:|------------------:|---------------:|--------:|---------------:|------------------:|-----------------:|--------------:|-----------------:|--------------------:|-------------------:|
| gsm8k      |        2 |               0 |                  0 |                 0 |            256 |       2 |              0 |                 0 |                0 |         256   |                0 |                   0 |                  0 |
| strategyqa |        2 |               0 |                  0 |                 0 |            192 |       2 |              0 |                 0 |                0 |          99.5 |                0 |                   0 |                  0 |

## Notes

- Residual stream representations are visualised for two random questions per benchmark total.
- Sequence dynamics plot token-by-token processing states in the final layer.
- The code uses HF hidden states directly and avoids TransformerLens cache paths.
- GSM8K uses gsm8k first and openai/gsm8k as a fallback.
- The code loads only one model at a time to avoid Kaggle OOMs.
- Verbose timestamps and GPU memory reports are included around expensive steps.