# SFT Champion Documentation

This folder documents the plain SFT checkpoint that currently serves as the strongest and safest model in the project.

The key result is that the SFT model is the current champion:
- GSM8K = 0.850
- StrategyQA = 0.660
- MMLU = 0.567

This matters because the project’s later RL experiments were evaluated against this model, and the evidence showed that the strongest gains came from better evaluation, better extraction, and better prompting rather than from generic reward optimization.

## What this folder explains

- why SFT was the right anchor model
- how the SFT objective was structured
- how the task prompts and answer formats were designed
- how the model was evaluated
- why the SFT checkpoint became the champion
- what the residual-stream analysis says about its behavior
- how to reproduce the results

## Why SFT is emphasized

The mechanistic experiments show that SFT improves the model mainly by:
- strengthening late-layer answer routing on GSM8K,
- improving decision sharpness and prompt discipline on StrategyQA,
- and making the final answer boundary more stable and benchmark-friendly.

That means SFT is not just “a training checkpoint.”  
It is the best evidence-backed baseline for the rest of the project.

## How to read this folder

Start with:
1. `01_sft_story.md`
2. `02_sft_objective_and_recipe.md`
3. `03_sft_data_prompting_and_evaluation.md`
4. `04_sft_results_and_champion_analysis.md`
5. `05_sft_mechanistic_evidence.md`
6. `06_sft_reproducibility.md`
7. `07_sft_figure_index.md`