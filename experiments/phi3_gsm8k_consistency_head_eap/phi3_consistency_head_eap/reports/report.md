# Consistency-head experiment report

- Model: `microsoft/phi-3-mini-4k-instruct`
- Samples: 40
- Consistency layers studied: [14, 15, 16, 17, 18]
- Prefix attention window: 8
- Patch window: 12

## Summary table

| Mode | Clean acc | Corrupt acc | Clean logprob | Corrupt logprob | Delta logprob |
|---|---:|---:|---:|---:|---:|
| anchored | 0.125 | 0.150 | -1.449 | -1.446 | -0.003 |
| plain | 0.150 | 0.150 | -1.805 | -1.796 | -0.009 |

## Observations

- **anchored**: strongest patch recovery at layer 14 (recovery 0.004).
- **anchored**: strongest DLA delta at layer 21 (delta 0.047).
- **anchored**: strongest attention-prefix delta at layer 16 (delta 0.001).
- **plain**: strongest patch recovery at layer 14 (recovery 0.017).
- **plain**: strongest DLA delta at layer 19 (delta 0.040).
- **plain**: strongest attention-prefix delta at layer 14 (delta 0.002).

## Files saved

- `csv/samples.csv`
- `csv/patch_rows.csv`
- `csv/attention_rows.csv`
- `csv/eap_rows.csv`
- `csv/tokenization.csv`
- `csv/dla_rows.csv`
- `plots/*.png`
- `reports/summary.json`, `reports/report.md`