# Failure-Driven Model Research

A reusable ChatGPT Skill for rigorous domain-model research, especially when adapting strong pretrained/SOTA image or video generation models to specialized domains.

The workflow enforces:

**baseline freeze -> failure discovery -> quantification -> functional localization -> falsifiable mechanism hypothesis -> causal intervention -> minimal patch -> ablation/generalization**

It is designed to prevent a common research failure mode: inventing a named module first and searching for evidence afterward.

## Skill contents

```text
failure-driven-model-research/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── diagnosis-protocol.md
    ├── evidence-levels.md
    ├── experiment-design.md
    └── research-ledger-template.md
```

## Core gates

- No stable failure -> do not invent a method.
- Correlation alone -> do not claim a causal mechanism.
- No discriminative intervention -> do not start expensive full training.
- Prefer reversible, zero-impact/identity-preserving additions before backbone modification.
- Always test target hard cases and normal cases for regressions.
- Record rejected hypotheses and negative experiments.

## Typical usage

Ask ChatGPT to use the Skill while working on a research project, for example:

> Use Failure-Driven Model Research to diagnose why my SOTA video baseline loses color fidelity on dense mural line drawings. Inspect available code/logs, reconstruct prior experiments, and choose the next minimal discriminative experiment.

or:

> Continue this model research using the failure-driven workflow. Do not propose a new module until the active mechanism hypothesis reaches intervention-level evidence.

When an execution connector such as AgentDockNew is available and authorized, the Skill instructs the assistant to inspect code, logs, checkpoints, results, and run minimal experiments directly instead of asking the user to manually paste information.
