# SFT data, prompting, and evaluation

This file explains the data flow that made the SFT checkpoint trustworthy.

## 1. Data structure

The SFT stage uses benchmark-style supervised examples that are formatted to match the final evaluation tasks:
- GSM8K: reasoning plus final numeric answer
- StrategyQA: binary yes/no answer
- MMLU: multiple-choice answer with a single letter output

The core idea is to make the training target look like the evaluation target.

## 2. Prompt design

The prompt is structured so that the model sees:
- a system instruction,
- a benchmark-specific user query,
- and a constrained answer format.

That is important because the model’s performance is highly sensitive to prompt structure. The earlier experiments showed that prompt form changes the causal route through the network, so the SFT prompt must be designed carefully.

## 3. Why extraction matters

The evaluation pipeline showed that extraction bugs can dramatically distort scores.

The project explicitly discovered that:
- MMLU could be undercounted if the extractor returned the first visible option letter,
- GSM8K could be undercounted if reasoning was truncated too early,
- and StrategyQA could be undercounted if outputs were not parsed robustly.

The later validated benchmark pipeline fixed those issues and produced the champion SFT scores. 

## 4. Evaluation protocol

The benchmark evaluation is not a training reward loop.
It is a separate scoring pipeline that does the following:

- GSM8K:
  1. generate reasoning
  2. extract the final numeric answer
  3. check exact match

- StrategyQA:
  1. generate reasoning
  2. extract yes/no
  3. check accuracy

- MMLU:
  1. generate MCQ response
  2. extract A/B/C/D
  3. check accuracy

This separation is important because the project repeatedly found that benchmark quality can change the apparent ranking of models.

## 5. Sampling policy

The SFT documentation should make clear that the final evaluation is based on correct benchmark handling, not on accidental first-N slices or brittle answer extraction.

The project’s later documentation emphasizes that:
- random sampling is better than first-N evaluation,
- robust extraction is better than naive letter matching,
- and holding the evaluation protocol fixed is essential for fair comparison.

## 6. Why the prompt-and-evaluation pipeline is part of the model story

A key lesson of the project is that the model and the evaluator are not separable in practice.
If evaluation is wrong, the model appears weaker than it is.
If evaluation is robust, the true SFT strength becomes visible.

That is why the SFT documentation must describe both the training recipe and the benchmark pipeline together.

## 7. Summary

The SFT champion is strong not only because of the weights, but because the surrounding data and evaluation pipeline are now correct enough to reveal the model’s real behavior.