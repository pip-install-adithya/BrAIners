# Task-specific residual stream behavior: GSM8K vs StrategyQA

This chapter zooms in on the two tasks that most clearly exposed the model’s internal behavior during the TLens analysis: GSM8K and StrategyQA.

The reason for separating them is simple. The two tasks do not fail in the same way:

- **GSM8K** is primarily a structured reasoning and final-answer routing problem.
- **StrategyQA** is primarily a calibration, commitment, and termination problem.

The residual-stream dashboards make this distinction very clear.  
Both tasks show late-layer answer commitment, but the shape of that commitment is different.

---

# 1. GSM8K behavior

## 1.1 What the base model is doing

Across the GSM8K dashboards, the base model shows a fairly strong late-layer collapse. The key signal is that the model builds a rich internal state, but its final answer selection is not always cleanly separated from the reasoning trace.

The main structural pattern in BASE is:

- residual norms rise steadily and then accelerate sharply in the final layers,
- entropy remains relatively high for much of the stack and then collapses late,
- the top-1 confidence rises abruptly near the end,
- the answer token appears late rather than being cleanly prepared throughout the stack,
- the PCA trajectory shows a broad exploratory path that turns sharply only near the end.

That makes the base model look like a system that can do a fair amount of internal computation, but still has difficulty converting that computation into a clean final answer route.

The most important observation is that the base model often appears to **hard-collapse** into an answer rather than **smoothly route** into it.  
That distinction matters because hard collapse can still produce the right token, but it is usually less stable, less interpretable, and more sensitive to prompt or decoding changes.

## 1.2 What the SFT model is doing

The SFT GSM8K dashboards show a more disciplined version of the same computation.

The most visible changes are:

- the answer token becomes salient more deliberately in the later layers,
- the model retains uncertainty a little longer before committing,
- the final answer emerges through a clearer late-stage selection process,
- the logit-lens heatmap shows more concentrated activation on the correct answer token,
- the convergence-to-final plot shows a more structured transition into the final distribution,
- the PCA path looks slightly more spread out before the final turn, which suggests richer intermediate processing.

This is the key mechanistic point:

**SFT does not simply make GSM8K “more confident.” It makes GSM8K more controlled.**

The model seems to spend the late layers doing a better job of separating reasoning content from answer emission. That is exactly what you would want on GSM8K, where the model must first reason through the problem and only then emit a final numeric answer.

## 1.3 Detailed comparison: BASE vs SFT on GSM8K

### Calibration and uncertainty
In the BASE plots, the final distribution collapses very aggressively. Entropy drops hard near the end and top-1 confidence becomes nearly saturated. That means the model commits strongly, but not necessarily in the most structured way.

In the SFT plots, the model stays uncertain for longer and then compresses more cleanly near the end. The entropy trajectory is not just lower or higher; it is **better shaped**. That is important because the model should preserve internal evidence until it is actually ready to finalize the number.

### Residual norm growth
Both models show the same general late growth pattern, but SFT tends to show a stronger and more meaningful late-layer contribution. This suggests that the model is doing more of the “answer consolidation” work in the later layers rather than collapsing earlier.

### Logit-lens behavior
The GSM8K logit-lens heatmaps are one of the most useful figures in the archive.

In BASE:
- answer tokens become visible late,
- but the transition is messy,
- and the model can briefly overfocus on the wrong local structure before settling.

In SFT:
- the correct answer token is pushed through the stack more deliberately,
- the late layers are doing clearer routing work,
- and the final answer token becomes visibly dominant in a more controlled way.

That means SFT improves not just the result, but the **mechanism of result formation**.

### PCA trajectory
The PCA plots suggest a two-stage process in both versions:
1. an exploratory phase where the residual stream moves through a broad internal path,
2. a final compression phase where the answer manifold is selected.

The SFT trajectory appears slightly richer before the final turn.  
The BASE trajectory looks more direct, but also more brittle.  
That is usually a sign that the base model is over-committing without fully stabilizing the internal route.

### Convergence to final distribution
This is the cleanest “decision shape” plot.

In BASE, the convergence happens more abruptly and more aggressively.  
In SFT, the hidden states approach the final answer distribution more gradually, which suggests the model is refining the answer rather than forcing it.

That difference is exactly why the SFT model feels better aligned with GSM8K.  
The task is not just to guess a number; it is to carry reasoning all the way to a stable final value.

## 1.4 GSM8K conclusion

The GSM8K evidence supports the following interpretation:

**The base model can often build enough internal structure to solve parts of the problem, but SFT makes the final answer routing cleaner, more selective, and more stable.**

So for GSM8K, the real gain from SFT is not only correctness.  
It is the reduction of routing noise and the strengthening of late-layer answer consolidation.

---

# 2. StrategyQA behavior

## 2.1 What the base model is doing

StrategyQA is different from GSM8K. The answer is not a number; it is a binary commitment. That changes the failure mode.

The base model on StrategyQA tends to behave like this:

- it builds a useful internal state across the stack,
- it often contains the right answer signal,
- but it does not always commit cleanly,
- entropy collapses late, but sometimes with visible wobble,
- top-1 confidence rises toward the end but can be less controlled than on SFT,
- the final output sometimes looks like a decision that was reached late and somewhat abruptly.

In other words, StrategyQA is less about constructing a long chain of arithmetic reasoning and more about **whether the model can settle on a yes/no decision and actually emit it**.

The base model often has the latent signal.  
What it lacks is stable decision commitment.

## 2.2 What the SFT model is doing

The SFT model improves exactly that part of the process.

The SFT StrategyQA dashboards show:

- a cleaner confidence collapse,
- lower entropy by the final layers,
- stronger selection of the correct `yes` or `no` token,
- more stable answer emission,
- and less evidence of last-minute indecision.

This is important because StrategyQA is often not a “know / do not know” benchmark. The model often knows enough to be right, but the output is not always cleanly aligned with the benchmark’s expected answer format.

SFT improves the model’s **commitment behavior**.  
That is why the SFT StrategyQA plots look more disciplined even when the raw answer is already correct.

## 2.3 Detailed comparison: BASE vs SFT on StrategyQA

### Calibration and commitment
The strongest difference is in the uncertainty curve.

In BASE:
- entropy decreases only after a relatively long uncertain phase,
- the model can hover around a partially resolved decision,
- and the final commitment feels more forced.

In SFT:
- the uncertainty remains visible for a while,
- but the model resolves the answer more cleanly at the end,
- and the final answer probability becomes much more decisive.

That makes SFT look like a model that is better at **decision finalization**.

### Answer-token routing
The logit-lens heatmaps show a stronger and cleaner late push toward the correct binary answer.  
This is especially visible when the correct answer is `yes`.

The SFT model does a better job of:
- boosting the right token late,
- suppressing competing tokens,
- and holding the correct answer route once it appears.

The BASE model can still get there, but the path is messier.

### Residual norm behavior
The residual norm growth is similar in overall shape, which means the model is not fundamentally changing its entire internal structure.  
The difference is in the **routing of the final decision**, not in the fact that the model is reasoning at all.

That is a key point because it says the task is not solved by “more computation” alone.  
It is solved by better final decision organization.

### PCA trajectory
The PCA trajectories again suggest the same broad pattern:
- a shared exploratory path,
- followed by a final turn into the answer region.

SFT looks slightly more organized near the final turn.  
The base model looks more like it arrives at the answer region by collapsing into it rather than moving smoothly.

### Convergence to final distribution
The convergence plot makes the StrategyQA story very clear.

SFT reaches the final distribution in a cleaner and more stable way.  
BASE reaches it too, but more noisily.  
That is exactly why SFT is the stronger checkpoint for StrategyQA: it better supports clean yes/no commitment.

## 2.4 StrategyQA conclusion

The StrategyQA evidence supports the following interpretation:

**The base model often has enough latent evidence to answer correctly, but SFT improves calibration, answer commitment, and final decision stability.**

So for StrategyQA, SFT is not just a “better predictor.”  
It is a better decider.

---

# 3. Cross-task interpretation

The two tasks together tell a very important story.

## GSM8K
- more about structured reasoning,
- answer routing,
- final numeric consolidation,
- late-stage token selection,
- and preserving the reasoning trace until the answer is ready.

## StrategyQA
- more about confidence,
- commitment,
- termination,
- and clean binary answer selection.

That distinction explains why the same SFT checkpoint improves both tasks, but in different ways.

### For GSM8K:
SFT improves the internal route from reasoning to number.

### For StrategyQA:
SFT improves the route from uncertainty to committed yes/no.

So the SFT checkpoint is not just globally better.  
It is better in a task-appropriate way.

---

# 4. Why this file belongs after the TLens capstone

This file is more specific than the capstone synthesis file.  
The capstone synthesis says what the project means overall.  
This file explains how the two most important tasks behave individually at the residual-stream level.

That makes it a good final TLens chapter because it gives the reader:
- the task-specific GSM8K story,
- the task-specific StrategyQA story,
- and the mechanistic reason the SFT model is the stable champion.

---

# 5. Figures to embed

## Task-Specific Residual Stream Interpretability Breakdowns

### 1. GSM8K Mechanical Topography

#### Base Model Reference Baselines
| Sample 0 Latent Stream Trace |
| :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights/phi3_residual_stream_deep_insights/plots/base/gsm8k_0_dashboard.png" width="85%" alt="GSM8K Sample 0 Base Dashboard"> |

| Sample 1 Latent Stream Trace |
| :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights/phi3_residual_stream_deep_insights/plots/base/gsm8k_1_dashboard.png" width="85%" alt="GSM8K Sample 1 Base Dashboard"> |

#### SFT Alignment Topography
| Sample 0 Post-SFT Stream Map |
| :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights/phi3_residual_stream_deep_insights/plots/sft/gsm8k_0_dashboard.png" width="85%" alt="GSM8K Sample 0 SFT Dashboard"> |

| Sample 1 Post-SFT Stream Map |
| :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights/phi3_residual_stream_deep_insights/plots/sft/gsm8k_1_dashboard.png" width="85%" alt="GSM8K Sample 1 SFT Dashboard"> |

#### Layerwise Logit Scaling & Token Reading Projections
| Sample 0 Cross-Model Logit Attribution |
| :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights/phi3_residual_stream_deep_insights/plots/comparison/gsm8k_0_comparison.png" width="85%" alt="GSM8K Sample 0 Inter-Model Comparison"> |

| Sample 0 Per-Token Sequence Dynamics |
| :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights/phi3_residual_stream_deep_insights/plots/comparison/gsm8k_0_sequence_dynamics.png" width="85%" alt="GSM8K Sample 0 Sequence Reading Dynamics"> |

| Sample 1 Cross-Model Logit Attribution |
| :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights/phi3_residual_stream_deep_insights/plots/comparison/gsm8k_1_comparison.png" width="85%" alt="GSM8K Sample 1 Inter-Model Comparison"> |

| Sample 1 Per-Token Sequence Dynamics |
| :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights/phi3_residual_stream_deep_insights/plots/comparison/gsm8k_1_sequence_dynamics.png" width="85%" alt="GSM8K Sample 1 Sequence Reading Dynamics"> |

---

### 2. StrategyQA Mechanical Topography

#### Base Model Reference Baselines
| Sample 0 Latent Stream Trace |
| :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights/phi3_residual_stream_deep_insights/plots/base/strategyqa_0_dashboard.png" width="85%" alt="StrategyQA Sample 0 Base Dashboard"> |

| Sample 1 Latent Stream Trace |
| :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights/phi3_residual_stream_deep_insights/plots/base/strategyqa_1_dashboard.png" width="85%" alt="StrategyQA Sample 1 Base Dashboard"> |

#### SFT Alignment Topography
| Sample 0 Post-SFT Stream Map |
| :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights/phi3_residual_stream_deep_insights/plots/sft/strategyqa_0_dashboard.png" width="85%" alt="StrategyQA Sample 0 SFT Dashboard"> |

| Sample 1 Post-SFT Stream Map |
| :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights/phi3_residual_stream_deep_insights/plots/sft/strategyqa_1_dashboard.png" width="85%" alt="StrategyQA Sample 1 SFT Dashboard"> |

#### Layerwise Logit Scaling & Token Reading Projections
| Sample 0 Cross-Model Logit Attribution |
| :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights/phi3_residual_stream_deep_insights/plots/comparison/strategyqa_0_comparison.png" width="85%" alt="StrategyQA Sample 0 Inter-Model Comparison"> |

| Sample 0 Per-Token Sequence Dynamics |
| :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights/phi3_residual_stream_deep_insights/plots/comparison/strategyqa_0_sequence_dynamics.png" width="85%" alt="StrategyQA Sample 0 Sequence Reading Dynamics"> |

| Sample 1 Cross-Model Logit Attribution |
| :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights/phi3_residual_stream_deep_insights/plots/comparison/strategyqa_1_comparison.png" width="85%" alt="StrategyQA Sample 1 Inter-Model Comparison"> |

| Sample 1 Per-Token Sequence Dynamics |
| :---: |
| <img src="../../src/t_lens/phi3_residual_stream_deep_insights/phi3_residual_stream_deep_insights/plots/comparison/strategyqa_1_sequence_dynamics.png" width="85%" alt="StrategyQA Sample 1 Sequence Reading Dynamics"> |

---

# 6. Final takeaway

If you want one compact interpretation of this file, it is this:

**GSM8K is a late-answer-routing problem, and StrategyQA is a calibration-and-commitment problem. SFT improves both by making the residual stream’s final decision pathway cleaner, more stable, and more selectively routed.**

That is the mechanistic reason the plain SFT model remains the strongest submission candidate.