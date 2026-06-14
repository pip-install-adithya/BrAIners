# STRATEGYQA delimiter causality report

| Metric | Clean | Corrupt | Delta |
|---|---:|---:|---:|
| Exact accuracy | 0.625 | 0.500 | +0.125 |
| Mean gold logprob | -2.607 | -1.905 | -0.702 |
| Mean prompt tokens | 54.8 | 53.8 | +1.0 |

## Key observations

- Strongest patch recovery layer: **1** (normalized recovery 1.162).
- Strongest DLA delta layer: **31** (delta 0.670).