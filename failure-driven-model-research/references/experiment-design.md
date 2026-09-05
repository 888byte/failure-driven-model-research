# Experiment Design

## Choose experiments by information gain

Prefer experiments that make competing hypotheses predict different outcomes.

Example:
- H1: matching is the bottleneck.
- H2: value/injection is the bottleneck.

High-information tests:
- oracle address with native value/injection;
- native address with oracle value;
- oracle both.

A generic longer training run is lower information because improvement or failure does not distinguish H1 from H2.

## Minimal experiment template

Define before execution:
- hypothesis under test;
- changed variable;
- fixed variables;
- samples/seeds;
- primary metric;
- preservation metric;
- expected direction under each hypothesis;
- support threshold;
- reject/deprioritize threshold;
- maximum compute/time budget.

## Use paired comparisons

When possible, compare baseline and intervention on exactly the same inputs, seeds, prompts, checkpoints, and evaluator versions.

## Use dose-response before a large search

For a suspected control strength, try a small ordered set such as low/base/high. A monotonic or threshold response is often more informative than a wide random hyperparameter sweep.

## Negative controls

Include a control intervention that should not fix the failure. If both the targeted intervention and the negative control improve similarly, the proposed mechanism is weak.

## Oracle tests

Oracle tests are diagnostic tools, not deployable methods.

Interpretation:
- oracle fixes failure -> the replaced component/path is plausibly limiting;
- oracle does not fix failure -> do not assume a better learned version of that component will help;
- oracle improves target metric but hurts preservation metric -> bottleneck may be real but requires constrained integration.

## Stop rules

Stop a direction when:
- predicted response repeatedly fails;
- only one sample or seed benefits;
- a simple alternative matches the gain;
- required intervention strength is so large that baseline capabilities collapse;
- additional tuning changes the story instead of testing it.
