# Diagnosis Protocol

## 1. Build a failure taxonomy before a method

For domain video/image generation, separate failures such as:
- structure deformation;
- color/reference mismatch;
- temporal flicker or drift;
- identity binding swap;
- texture/style collapse;
- motion under-control or over-control;
- static freeze;
- background/foreground leakage;
- long-horizon degradation.

Assign one primary metric and one preservation metric to each important failure.

## 2. Construct stress variables

Choose factors that have domain meaning and can be measured or controlled. Examples:
- edge/line density;
- local entropy or texture frequency;
- motion magnitude/acceleration;
- occlusion ratio;
- number of controlled objects;
- reference-target chroma gap;
- prompt complexity;
- temporal length;
- spatial distance from known context;
- control-map sparsity.

Prefer 2-4 levels per factor before attempting a large factorial design.

## 3. Localize by function

Use interventions that isolate pathways:
- zero a condition branch;
- scale one condition only;
- freeze or bypass a module;
- substitute oracle correspondence;
- substitute oracle value/feature;
- keep address fixed while changing value, or vice versa;
- perturb only one input modality;
- compare early vs late injection;
- inspect feature norm, entropy, similarity, saturation, routing load, or gradient norm where meaningful.

## 4. Use counterfactual tests

A strong counterfactual changes only the variable that should matter.

Examples:
- recolor the reference while preserving structure;
- keep the same trajectory and change subject identity;
- keep the same first frame and vary motion magnitude;
- keep control strength fixed and vary line density;
- use the same sample with/without oracle matching.

Ask whether the output changes in the predicted direction.

## 5. Distinguish component failure from capacity failure

Before adding capacity, test whether the existing component receives the correct information.

Useful sequence:
1. oracle input to existing component;
2. stronger/weaker existing signal;
3. small residual correction;
4. only then larger/new module.

If an oracle does not fix the failure, do not build a better estimator for that oracle quantity until another bottleneck is excluded.

## 6. Preserve a normal set

Every hard/failure subset must have a normal/control subset. A patch that improves the hard set while materially degrading the normal set is not a clean fix.

## 7. Diagnose stochastic effects

If generation is stochastic:
- hold seeds fixed for paired comparisons;
- then evaluate multiple seeds for robustness;
- distinguish best-of-N improvement from average improvement;
- do not interpret a lucky seed as mechanism evidence.
