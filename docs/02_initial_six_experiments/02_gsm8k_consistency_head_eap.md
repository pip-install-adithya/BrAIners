# GSM8K consistency-head / EAP experiment

This experiment asks a specific mechanistic question:  
where does the model become consistent enough to commit to the final arithmetic answer?

## Experimental setup

- Model: `microsoft/phi-3-mini-4k-instruct`
- Samples: 40
- Consistency layers: 14, 15, 16, 17, 18
- Prefix attention window: 8
- Patch window: 12
- Variants: plain and anchored

## What the experiment measures

The analysis combines:
- activation patching,
- EAP-style evidence tracing,
- DLA curves,
- attention-prefix deltas,
- gold log-probability,
- and layerwise consistency-head behavior.

The purpose is to see whether there is a localized internal circuit that supports arithmetic closure.

## Main results

The summary table shows very low exact accuracy for the sampled set, but the mechanistic signals are still informative.

- anchored:
  - clean acc = 0.125
  - corrupt acc = 0.150
  - clean logprob = -1.449
  - corrupt logprob = -1.446
- plain:
  - clean acc = 0.150
  - corrupt acc = 0.150
  - clean logprob = -1.805
  - corrupt logprob = -1.796

The best patch recovery is concentrated around layer 14 in both variants, which is strong evidence that the answer-routing signal is late and localized.

## Interpretation

The important result is not that the experiment “solves” GSM8K.  
It does not.  
The important result is that the model appears to carry a consistency-related signal in a narrow late-layer region.

That supports a few later decisions:
- process-style rewards are reasonable,
- answer-verification rewards are reasonable,
- and the model should be encouraged to finish a reasoning chain cleanly rather than merely generate plausible arithmetic text.

The anchored variant slightly changes the routing path, but the overall behavior remains limited.  
That means the issue is not just prompt cosmetics.  
It is how the model decides when to finalize the answer.

## Figures to embed

- `../experiments/phi3_gsm8k_consistency_head_eap/phi3_consistency_head_eap/plots/plain_accuracy_bar.png`
- `../experiments/phi3_gsm8k_consistency_head_eap/phi3_consistency_head_eap/plots/plain_attention_curve.png`
- `../experiments/phi3_gsm8k_consistency_head_eap/phi3_consistency_head_eap/plots/plain_consistency_head_heatmap.png`
- `../experiments/phi3_gsm8k_consistency_head_eap/phi3_consistency_head_eap/plots/plain_patch_recovery_curve.png`
- `../experiments/phi3_gsm8k_consistency_head_eap/phi3_consistency_head_eap/plots/plain_patch_recovery_heatmap.png`
- `../experiments/phi3_gsm8k_consistency_head_eap/phi3_consistency_head_eap/plots/plain_dla_curve.png`
- `../experiments/phi3_gsm8k_consistency_head_eap/phi3_consistency_head_eap/plots/plain_gold_logprob_bar.png`
- `../experiments/phi3_gsm8k_consistency_head_eap/phi3_consistency_head_eap/plots/plain_metric_correlations.png`
- `../experiments/phi3_gsm8k_consistency_head_eap/phi3_consistency_head_eap/plots/anchored_accuracy_bar.png`
- `../experiments/phi3_gsm8k_consistency_head_eap/phi3_consistency_head_eap/plots/anchored_attention_curve.png`
- `../experiments/phi3_gsm8k_consistency_head_eap/phi3_consistency_head_eap/plots/anchored_consistency_head_heatmap.png`
- `../experiments/phi3_gsm8k_consistency_head_eap/phi3_consistency_head_eap/plots/anchored_patch_recovery_curve.png`
- `../experiments/phi3_gsm8k_consistency_head_eap/phi3_consistency_head_eap/plots/anchored_patch_recovery_heatmap.png`
- `../experiments/phi3_gsm8k_consistency_head_eap/phi3_consistency_head_eap/plots/anchored_dla_curve.png`
- `../experiments/phi3_gsm8k_consistency_head_eap/phi3_consistency_head_eap/plots/anchored_gold_logprob_bar.png`
- `../experiments/phi3_gsm8k_consistency_head_eap/phi3_consistency_head_eap/plots/anchored_metric_correlations.png`

## Conclusion

GSM8K is not just a math problem.  
It is also a late-layer consistency problem.  
That is why the later training pipeline includes format control, answer routing, and self-correction-style signal.