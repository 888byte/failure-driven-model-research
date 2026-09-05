# Evidence Levels

Use this scale to prevent claims from outrunning evidence.

## E0 - Anecdotal observation

Evidence: one or a few examples, qualitative impression, or an unexplained metric change.

Allowed claim: a possible failure worth testing.

Not allowed: mechanism, causal language, or method justification.

## E1 - Repeatable association

Evidence: the failure repeats across multiple samples/seeds or correlates with a controlled domain factor.

Examples:
- error rises with line density;
- long sequences fail more often than short ones;
- a hard subset consistently underperforms an easy subset.

Allowed claim: factor X is associated with failure Y.

Not allowed: X causes Y.

## E2 - Controlled intervention evidence

Evidence: changing the suspected causal factor while holding major alternatives fixed produces the predicted change.

Examples:
- increasing structure-condition scale worsens color error monotonically;
- oracle correspondence removes most of the failure while value injection is unchanged;
- disabling one branch removes a specific artifact.

Allowed claim: results support the proposed mechanism.

## E3 - Repeated mechanism evidence

Evidence: intervention is replicated across samples/seeds/settings and competing explanations are tested or materially weakened.

Expected additions:
- dose-response or multiple intervention strengths;
- negative control;
- simple alternative baseline;
- preservation metric.

Allowed claim: mechanism is strongly supported in the studied setting.

## E4 - Cross-setting validation

Evidence: E3 plus generalization across another dataset, domain split, baseline family, or meaningful operating regime when relevant.

Allowed claim: strong paper-level mechanism/generalization statement, still bounded to tested conditions.

## Confidence rule

Report confidence independently from evidence level.

- Low: major competing explanations remain.
- Medium: evidence is coherent but incomplete.
- High: repeated interventions and controls consistently support the same explanation.

Never label E0/E1 as High causal confidence.
