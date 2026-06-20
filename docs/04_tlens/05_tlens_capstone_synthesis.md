# TLens capstone synthesis

This chapter is the final mechanistic synthesis for the project.

The earlier six experiments established the basic failure modes:
- delimiter sensitivity,
- late arithmetic routing,
- calibration gaps,
- answer-slot bias,
- unstable self-correction,
- and shared but not identical task geometry.

The advanced five then turned those observations into a deeper atlas:
- prompt form as intervention,
- StrategyQA as a stability basin,
- MMLU as a permutation lattice,
- self-correction as a conditional recovery process,
- and task families as distinct geometric regions.

This TLens section closes the loop by showing how those same themes appear in the residual stream and in the checkpoint trajectory of the model itself.

## What the full mechanistic story says

1. **The base model is not blank.**  
   It already contains useful latent reasoning structure.

2. **The core bottleneck is answer routing.**  
   The network often builds signal internally, but the final answer token becomes reliable only late in the residual stream.

3. **SFT improves the interface, not just the score.**  
   It makes the route to the final answer cleaner and more decisive.

4. **HGRPO changes the trajectory, but does not fully dominate SFT.**  
   It shows that the model is steerable, but also that reward-only movement can reshape behavior without cleanly beating the best supervised checkpoint.

5. **The advanced experiments justify the next model choice.**  
   Because the failure is structured, the best next-step challenger is not generic RL scaling. It is a hard-mined, routing-aware refinement stage that targets the examples and answer routes that still fail.

## Why this chapter matters for the submission

This folder is the final bridge between:
- the evaluation story,
- the mechanistic story,
- and the solution story.

It explains why the project should present:
- the plain SFT checkpoint as the stable champion,
- and the RRPO hard-mining checkpoint as the most novel and principled follow-up.

## Final interpretation

The combined evidence across all folders supports a single claim:

**Phi-3-mini is not fundamentally unable to solve these tasks; it is often unable to route its internal signal into the correct final decision in a stable, benchmark-aligned way.**

That is why the final intervention design focuses on:
- answer commitment,
- format discipline,
- calibration,
- permutation robustness,
- and hard-example mining.

## Closing sentence

The TLens folder should be read last, because it is the capstone mechanistic proof that connects every earlier experiment into one coherent project narrative.