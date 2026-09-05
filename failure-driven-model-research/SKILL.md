---
name: failure-driven-model-research
description: Run rigorous failure-driven research for adapting large pretrained or SOTA models to specialized domains, especially generative vision/video systems. Use when the user wants to diagnose a baseline, discover domain-specific failure modes, locate likely mechanisms, design causal interventions, propose minimal architectural or training changes, validate innovations, plan ablations, or continue an existing research project. Enforce evidence gates before method invention, preserve a reproducible baseline, prefer minimal discriminative experiments, and use available execution connectors (such as AgentDockNew or equivalent) to inspect code, logs, checkpoints, and results when authorized.
---

# Failure-Driven Model Research

Use a failure-first scientific workflow. Do not begin by inventing modules. Establish what fails, under which conditions, why the proposed mechanism is plausible, and whether a minimal intervention changes the failure before modifying a strong backbone.

## Core operating rules

1. Preserve a reproducible baseline before changing the model.
2. Separate observation, correlation, mechanism hypothesis, causal evidence, and validated method.
3. Change one causal factor at a time whenever practical.
4. Prefer the cheapest experiment that best distinguishes competing hypotheses.
5. Prefer local, reversible, identity-preserving interventions over backbone rewrites.
6. Keep rejected hypotheses and negative results in the research ledger.
7. Do not claim a mechanism as proven from benchmark improvement alone.
8. Do not continue tuning a hypothesis indefinitely after repeated reasonable falsification.
9. Check recent literature and the current baseline before making a novelty claim.
10. If execution tools are available and the user has authorized research execution, inspect and run the minimal experiment rather than only suggesting it.

## Start by reconstructing state

For an existing project, first recover the current research state from available conversation context, files, repository, experiment logs, or connected execution environment. Reuse valid evidence instead of restarting the workflow.

Record:
- baseline model/checkpoint and code revision;
- task and domain;
- fixed inference/training settings;
- datasets and evaluation subsets;
- metrics and acceptance thresholds;
- current modifications;
- completed experiments, including failures;
- active hypotheses and their evidence levels.

If any missing detail can be resolved through an available connector, inspect it directly before asking the user.

## Research workflow

Follow these stages. Advance only when the gate for the current stage is satisfied. See `references/diagnosis-protocol.md` for detailed experiment patterns and `references/evidence-levels.md` for evidence semantics.

### Stage 0 - Freeze the baseline

Create an immutable reference configuration for comparison.

Require, where applicable:
- checkpoint/model version;
- code commit or reproducible source state;
- prompt/conditioning inputs;
- random seeds;
- resolution/frame count/context length;
- sampler, steps, CFG/guidance and other inference settings;
- optimizer, LR, batch and training schedule for training comparisons;
- exact evaluation scripts and metric definitions.

Gate: baseline can be rerun or its results are otherwise reproducibly documented.

### Stage 1 - Discover failures

Do not modify the model yet. Construct a domain-relevant stress matrix and search for repeatable failure modes.

Vary interpretable domain factors such as:
- structural complexity;
- texture density;
- motion magnitude;
- occlusion;
- reference-target discrepancy;
- number of subjects;
- sequence length;
- color/style complexity;
- conditioning ambiguity.

Prefer controlled perturbations and stratified subsets over arbitrary cherry-picked examples.

Gate: identify at least one repeatable failure linked to a describable condition.

### Stage 2 - Quantify the failure

Turn visual impressions into measurable behavior.

For each candidate failure:
- choose a primary failure metric;
- track at least one preservation metric for abilities that must not regress;
- compare condition groups or continuous severity;
- report effect size, variability, and sample count when possible;
- inspect whether the relationship is monotonic, thresholded, or interaction-dependent.

Do not write "the model struggles with complex samples" when a measurable statement can be made.

Gate: the failure is statistically or repeatedly measurable and not explained by an uncontrolled setting change.

### Stage 3 - Functionally localize

Localize to a functional pathway before trying to localize individual parameters.

Test components such as:
- text condition;
- image/reference condition;
- structure/edge condition;
- motion/trajectory condition;
- temporal module;
- correspondence/matching component;
- adapter/control branch;
- attention or routing path;
- decoder/backbone.

Use toggles, scaling, replacement, oracle inputs, bypasses, frozen probes, or feature statistics.

Gate: narrow the failure to one or a small number of plausible functional pathways, or explicitly document that localization remains ambiguous.

### Stage 4 - Form competing mechanism hypotheses

Write at least one falsifiable hypothesis and, when uncertainty is material, at least one competing hypothesis.

For every hypothesis specify:
- observed failure;
- existing evidence;
- proposed mechanism;
- a prediction that would be true if the hypothesis is correct;
- a result that would weaken or reject it;
- likely confounders.

Do not create a named module in this stage.

Gate: hypothesis produces a discriminative, feasible prediction.

### Stage 5 - Run causal intervention

Design the smallest intervention that manipulates the suspected cause while holding unrelated factors fixed.

Preferred interventions include:
- condition-strength sweeps;
- feature clamping or normalization;
- branch disable/enable;
- oracle correspondence/address/value replacement;
- controlled masking;
- local reweighting;
- synthetic counterfactual inputs;
- targeted bypass or replacement.

Use the result to update the evidence level. A correlation is not upgraded to causal evidence without an intervention or equivalently strong identification strategy.

Gate: either obtain intervention evidence supporting the mechanism, or reject/deprioritize the hypothesis and return to Stage 3/4.

### Stage 6 - Design the minimal patch

Only now propose a method. Map each method component to a supported failure mechanism.

Use this intervention ladder from lowest to highest risk:
1. inference-time policy or calibration;
2. dynamic gate/reweighting;
3. zero-initialized residual adapter, LoRA, side branch, or small memory module;
4. modification of an existing local module;
5. backbone architectural change.

Prefer an identity-preserving form when possible, for example `y_new = y_base + alpha * delta`, initialized with `alpha = 0` or an equivalent zero-impact initialization.

Before claiming novelty, search current literature for equivalent mechanisms, especially in the same baseline family and adjacent domains. Distinguish domain novelty, mechanism novelty, and engineering adaptation.

Gate: proposed patch directly addresses evidence-backed mechanism and has a clear rollback path.

### Stage 7 - Validate method and side effects

Require more than "ours beats baseline".

Evaluate:
- target hard/failure subset;
- normal/easy subset to detect regressions;
- full benchmark or representative test set;
- component ablation;
- sensitivity to the key hyperparameters;
- multiple seeds when stochastic variance matters;
- at least one alternate dataset/domain split when generalization is part of the claim;
- compute, memory, latency, or parameter overhead when relevant.

Explicitly test simple alternatives that could explain the gain, such as stronger guidance, longer training, larger adapter, different seed, or extra data.

Gate: improvement survives ablation and does not create unacceptable regressions.

### Stage 8 - Convert evidence into a research claim

Write the contribution only at the strength supported by evidence.

Use calibrated claim language:
- observation: "we observe";
- correlation: "is associated with";
- intervention-supported mechanism: "results support the hypothesis that";
- validated method: "the proposed method improves ... under ...".

Never convert an E1 correlation into a definitive causal statement.

## Evidence gates

Use the evidence scale in `references/evidence-levels.md` and display the current level for each active hypothesis.

Minimum defaults:
- E0-E1: diagnose only; do not commit to architecture changes.
- E2: allow a minimal prototype if intervention results are consistent.
- E3: allow broader training and formal method development.
- E4: support strong paper-level mechanism/generalization claims.

These are defaults, not mathematical laws. Tighten them when experiments are expensive or the baseline is fragile.

## Experiment selection rule

When multiple experiments are possible, rank them by:
1. hypothesis discrimination power;
2. causal interpretability;
3. cost/time;
4. risk of corrupting the baseline;
5. reuse value for later paper evidence.

Prefer one high-information experiment over many weak sweeps. See `references/experiment-design.md`.

## Research ledger

Maintain a compact ledger throughout long projects using `references/research-ledger-template.md`.

Do not erase rejected directions. Record why they were rejected so future work does not repeat them.

## Tool and execution behavior

When code, server, logs, checkpoints, or generated outputs are available through a connected environment such as AgentDockNew:
1. inspect the current state before editing;
2. verify file paths, commands, GPU/process state, and current results;
3. execute the smallest diagnostic experiment first;
4. preserve the original configuration and checkpoint;
5. verify outputs after modification;
6. record exact commands/config deltas in the research ledger;
7. checkpoint progress during long multi-step work.

Do not ask the user to paste information that can be inspected directly through an authorized connector.

If execution access is unavailable, produce an executable experiment specification instead of pretending the experiment was run.

## Required response format during research

Unless the user asks for another format, finish each research iteration with these six fields:

**Current failure** - one precise statement of the failure being investigated.

**Evidence** - quantitative/qualitative evidence and the current evidence level.

**Current hypothesis** - the mechanism hypothesis, separated from established facts.

**Confidence** - Low/Medium/High plus E0-E4.

**Next minimal experiment** - the single experiment with the highest information value, including fixed variables and changed variable(s).

**Decision rule** - state in advance which outcomes support, weaken, or reject the hypothesis and what branch follows each result.

For completed method validation, additionally summarize target-set gain, normal-set regression, ablation result, overhead, and remaining risks.

## Stop and reconsider conditions

Stop tuning the current path and return to diagnosis when any of the following occurs:
- three or more reasonable intervention attempts fail to support the same mechanism without new evidence;
- gains occur only on cherry-picked examples;
- the target metric improves while preservation metrics degrade beyond an agreed threshold;
- an apparent gain disappears under fixed seeds/configuration;
- the method only works after changing multiple uncontrolled factors;
- literature search reveals the claimed novelty is already standard without a meaningful domain contribution.

The correct research outcome may be rejection of a hypothesis. Treat that as progress.
