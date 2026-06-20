# TLens Capstone: Residual Stream and Answer Routing Analysis

This folder is the mechanistic capstone of the project.  
The earlier six experiments establish the model’s basic failure modes; the five advanced experiments explain those failures more deeply through prompt causality, calibration basins, permutation fragility, self-correction dynamics, and task geometry. This TLens section then ties everything together by showing how the model’s residual stream changes across the base model, the strong SFT model, and the HGRPO checkpoint trajectory.

## Why this folder exists

The benchmark tables tell us *what* happened.  
The mechanistic atlas tells us *why* it happened.

This folder focuses on the answer-routing interface:
- how late the model commits to an answer,
- how sharply the answer token emerges,
- how confidence changes across depth,
- how SFT changes the residual stream geometry,
- and how the HGRPO checkpoints reshape behavior without fully surpassing the clean SFT champion.

## What to read first

1. `01_sft_residual_stream_safe_fixed.md`
2. `02_sft_residual_stream_deep_insights.md`
3. `03_hgrpo_multicheckpoint_residual_stream.md`
4. `04_tlens_capstone_synthesis.md`
5. `05_figure_index.md`

## What the figures show

The TLens archive contains:
- base-model dashboards,
- SFT dashboards,
- comparison dashboards,
- sequence-dynamics figures,
- and checkpoint progression figures.

The SFT runs are especially useful because they show that the main effect of supervised finetuning is not just higher accuracy, but cleaner final-answer routing and more structured late-layer commitment. The HGRPO run adds a training trajectory view, showing how the model changes checkpoint by checkpoint.

## Figure naming convention

The figures are stored with relative paths from `docs/`.  
Where the archive uses sample IDs, the sample IDs are preserved in the filenames, such as:
- `gsm8k_0`
- `gsm8k_1`
- `strategyqa_0`
- `strategyqa_1`

The HGRPO archive uses the same sample-ID convention across its checkpoint folders.

## Role in the final submission

This folder is not a replacement for the earlier experiments.  
It is the final mechanistic proof layer that makes the project story coherent:
- the baseline is weak for diagnosable reasons,
- SFT stabilizes the answer route,
- HGRPO changes the trajectory but does not fully displace the SFT champion,
- and the advanced experiments explain why hard-mining RRPO is the most sensible next challenger.