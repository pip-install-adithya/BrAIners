# GSM8K delimiter causality report

| Metric | Clean | Corrupt | Delta |
|---|---:|---:|---:|
| Exact accuracy | 0.375 | 0.500 | -0.125 |
| Mean gold logprob | -1.990 | -1.983 | -0.007 |
| Mean prompt tokens | 106.5 | 105.5 | +1.0 |

## Key observations

- Strongest patch recovery layer: **0** (normalized recovery 3.217).
- Strongest DLA delta layer: **32** (delta 0.876).