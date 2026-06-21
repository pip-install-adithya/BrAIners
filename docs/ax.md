# ax.md

## Agentic AI, open-weight models, and implementation workflow

This project was built around an open-weight model stack so that the entire reasoning pipeline could be inspected, modified, benchmarked, and reproduced end to end.

The core backbone was:

- `microsoft/phi-3-mini-4k-instruct`

The project then extended that backbone through:
- supervised finetuning,
- mechanistic interpretability,
- evaluation harnesses,
- calibration and extraction fixes,
- GRPO-style reinforcement learning experiments,
- hierarchical steering experiments,
- hard-example mining,
- and a final RRPO / DPO-style challenger.

The main idea was not to treat the model as a black box.  
Instead, the project treated it as a system with measurable failure modes:
- late answer routing,
- calibration collapse,
- option-order bias,
- extraction brittleness,
- and task-specific decision fragility.

That is why the implementation was organized as an agentic pipeline rather than a single training script.

---

## 1. Open-weight model strategy

The project intentionally used open-weight models for three reasons.

### 1.1 Reproducibility
The full stack had to be reproducible on the target platform.  
Open weights made it possible to:
- reload the exact base model,
- compare the SFT checkpoint against the baseline,
- inspect residual-stream behavior,
- and rerun benchmark evaluation consistently.

### 1.2 Inspectability
Because the project relied heavily on mechanistic interpretability, the backbone had to be open enough to:
- read hidden states,
- inspect token probabilities,
- compare layerwise behavior,
- and perform residual-stream analysis.

### 1.3 Training flexibility
The project needed to experiment with:
- LoRA / PEFT,
- hard-example mining,
- preference optimization,
- and steering-aware reward shaping.

That is only practical when the model is open and modifiable.

---

## 2. Agentic AI setup

The project was not a single agent in the “chatbot” sense.  
It was a **system of specialized agents / roles** that each handled one part of the workflow.

### 2.1 Data curation role
This role was responsible for:
- building train and evaluation pools,
- random sampling held-out sets,
- caching selected indices,
- and tracking hard examples.

This role ensured that the experiment was not accidentally biased by first-N selection or unstable sampling.

### 2.2 Evaluation role
This role was responsible for:
- generating predictions,
- extracting final answers,
- checking exact correctness,
- computing per-task metrics,
- and saving per-sample CSVs.

This was critical because the project repeatedly showed that evaluation bugs could distort the entire narrative.

### 2.3 Mechanistic analysis role
This role handled:
- TLens-style residual-stream dashboards,
- base vs SFT comparisons,
- task-specific trajectory analysis,
- confidence and entropy curves,
- and layerwise answer-routing inspection.

This role turned benchmark results into mechanistic evidence.

### 2.4 Training role
This role handled:
- SFT warmup,
- GRPO / hierarchical steering,
- preference-pair mining,
- hard-example weighting,
- and final RRPO / DPO-style refinement.

### 2.5 Reporting role
This role handled:
- figure saving,
- markdown documentation,
- CSV exports,
- summary tables,
- and the final project narrative.

---

## 3. Reasoning and planning pipeline

The pipeline evolved in stages, and each stage was motivated by the results of the previous one.

### Stage A: baseline evaluation
The first task was to measure what the model could already do.

The early baseline runs showed:
- GSM8K was not hopeless, but the model was unstable in final answer emission,
- StrategyQA was often a commitment / calibration problem,
- MMLU was heavily affected by parsing and option-order behavior.

This stage established the project’s core hypothesis:

\[
\text{the model has latent capability, but weak final routing}
\]

### Stage B: supervised finetuning
The next step was to make the output format and answer behavior more stable.

SFT was chosen because it is the most direct way to teach:
- task-specific answer structure,
- output discipline,
- and benchmark-compatible formatting.

### Stage C: mechanistic diagnosis
The TLens-style analyses then showed that the model’s main weakness is not raw reasoning alone.  
The bottleneck is the transition from:
\[
\text{internal reasoning state} \rightarrow \text{final answer token}
\]

That finding shaped all later training ideas.

### Stage D: RL experimentation
Generic GRPO was tried first because it is a natural way to optimize relative rollout quality.  
But the results showed that reward movement did not consistently translate into benchmark improvement.

That led to:
- hierarchical steering,
- then hard-example mining,
- then RRPO / DPO-style refinement.

### Stage E: final selection
The final project story became:
- **plain SFT checkpoint = stable champion**
- **RRPO hard-mining checkpoint = strongest RL-style challenger**

That is the most honest and defensible conclusion.

---

## 4. Tool use and tool chaining

The project used a chain of tools rather than one monolithic script.

### 4.1 Model loading
- Hugging Face `transformers`
- PEFT / LoRA
- bitsandbytes quantization where required
- cautious remote-code handling for Phi-3

### 4.2 Dataset handling
- Hugging Face `datasets`
- deterministic sampling
- cached random indices
- task-specific dataset loaders

### 4.3 Training harnesses
- supervised finetuning loop
- evaluation loop
- preference-pair mining loop
- online refinement loop
- per-stage checkpoints

### 4.4 Interpretability harness
- hidden-state capture
- token-probability tracking
- residual norm tracking
- cosine-to-final tracking
- dashboard plotting
- comparison figures

### 4.5 Reporting harness
- CSV exports
- JSON summary exports
- Markdown documentation
- figure indexing
- reproducibility notes

This chaining matters because each stage depends on the previous one:
- data curation feeds training,
- training feeds evaluation,
- evaluation feeds interpretation,
- interpretation feeds the next training design,
- and everything is archived for the report.

---

## 5. Coding assistants and development workflow

The project benefited from iterative code generation and debugging support.

### What worked
- breaking large scripts into smaller functions,
- keeping the model load / eval / train / plot pipeline separate,
- generating explicit CSV and plot artifacts at every stage,
- writing task-specific parsers,
- and making each experiment self-contained.

### What did not work
- overly large all-in-one notebooks,
- changing multiple core assumptions at once,
- using brittle extraction logic,
- and relying on generic reward objectives without mechanistic grounding.

The most productive workflow was:
1. inspect the failure,
2. identify the mechanistic bottleneck,
3. design a narrow intervention,
4. run a controlled benchmark,
5. save all outputs,
6. revise the next stage.

That is the actual agentic loop the project used.

---

## 6. Harness design

The project’s harnesses were deliberately split into separate components.

### 6.1 Benchmark harness
This harness handled:
- GSM8K,
- StrategyQA,
- MMLU,
- random sampling,
- answer parsing,
- exact-match scoring,
- and per-sample logging.

### 6.2 Training harness
This harness handled:
- SFT,
- GRPO,
- hierarchical steering,
- hard-mining preference optimization,
- and conservative updates.

### 6.3 Interpretation harness
This harness handled:
- residual-stream dashboards,
- per-layer summaries,
- task comparisons,
- and checkpoint comparisons.

### 6.4 Reporting harness
This harness handled:
- saving plots,
- saving summary tables,
- exporting markdown,
- and indexing all figures.

The split was important because each harness had a different failure mode.  
Keeping them separate made debugging and reproducibility much easier.

---

## 7. Memory and context handling

Because the backbone model is non-trivial in size, context management and memory handling were critical.

### 7.1 Memory strategy
The implementation used:
- 4-bit loading when appropriate,
- controlled device placement,
- `expandable_segments:True`,
- empty-cache calls,
- and conservative batch sizes.

### 7.2 Context strategy
The prompt and generation pipeline was kept compact:
- task-specific instructions,
- small few-shot sets,
- clear answer formatting,
- and controlled max-new-token limits.

### 7.3 Why this mattered
The project’s earlier failures showed that memory instability can completely derail an otherwise valid idea.  
So the engineering had to be practical, not just elegant.

---

## 8. Multi-agent orchestration

This project can be understood as a lightweight multi-agent system.

### Agent 1: benchmark sampler
Chooses samples and keeps the evaluation set fair.

### Agent 2: answer generator
Produces candidate completions from the model.

### Agent 3: parser / scorer
Extracts the final answer and determines correctness.

### Agent 4: trainer
Uses the scores to update the model.

### Agent 5: mechanistic observer
Tracks residual-stream behavior and interpretation plots.

### Agent 6: report compiler
Converts all outputs into a coherent documentation story.

The orchestration is not a distributed agent swarm in the strict infrastructure sense.  
But it is still agentic in design because the system decomposes the problem into specialized, cooperating roles.

---

## 9. Memory of what worked

The most effective choices were:

### 9.1 SFT with a clean answer format
This gave the model a stable benchmark-compatible behavior.

### 9.2 Robust evaluation
This revealed the model’s actual performance instead of an artifact of parsing mistakes.

### 9.3 TLens-style diagnosis
This made the key bottleneck visible:
the model’s late-layer answer routing.

### 9.4 Hard-example mining
This focused training on the most informative failures.

### 9.5 Preference optimization
This taught the model to prefer cleaner and more benchmark-compatible outputs.

### 9.6 Stage-wise design
This avoided the failure of trying to solve everything with one RL loop.

---

## 10. Memory of what did not work

The least effective choices were:

### 10.1 Flat generic GRPO
It improved the reward proxy without consistently improving the actual benchmarks.

### 10.2 Over-aggressive RL before stabilization
This could reshape behavior but not reliably beat the SFT champion.

### 10.3 Weak extraction logic
This caused large metric distortions, especially on MMLU.

### 10.4 Uniform reward pressure
The tasks are not the same, so a single reward was too coarse.

### 10.5 Universal self-correction
A second pass sometimes improved results, but often introduced regressions.

### 10.6 Ignoring task geometry
The representation space is not identical across GSM8K, StrategyQA, and MMLU.

---

## 11. What the project learned about agentic AI

The main lesson is that agentic systems do not need to be large to be useful.  
They need to be well decomposed.

A good agentic setup here:
- separates sampling from scoring,
- separates training from interpretation,
- separates evaluation from generation,
- and separates the stable champion from the exploratory challenger.

That made the project easier to reason about and easier to defend.

---

## 12. Final conclusion

The solution is an open-weight, agentically structured reasoning system built on Phi-3-mini.

Its strongest features are:
- transparent training stages,
- benchmark-specific evaluation,
- mechanistic interpretability,
- hard-example mining,
- and a clear split between the stable SFT champion and the RL-based challenger.

The most important realization was that the model’s remaining weakness is not a lack of general intelligence.  
It is the difficulty of converting internal reasoning into the right final answer route.

That is the problem the project is actually solving.