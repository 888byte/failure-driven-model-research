# Research Ledger Template

Keep one row per meaningful hypothesis or experiment family.

| ID | Date | Failure | Hypothesis | Evidence level | Experiment / intervention | Key result | Preservation result | Decision | Next action |
|---|---|---|---|---|---|---|---|---|---|
| H01 | YYYY-MM-DD | ... | ... | E1 | ... | ... | ... | continue/reject/hold | ... |

## Experiment record

For experiments that may be cited later, record:

- Experiment ID:
- Code revision / commit:
- Checkpoint:
- Dataset/subset:
- Sample IDs:
- Seeds:
- Fixed configuration:
- Changed variable(s):
- Command/config path:
- Primary metric:
- Preservation metric:
- Result:
- Interpretation:
- Evidence level before -> after:
- Decision:
- Artifact/output path:

## Decision vocabulary

Use one of:
- `CONTINUE`: evidence supports another targeted test.
- `PROMOTE`: evidence is strong enough to prototype a method.
- `HOLD`: ambiguous; another discriminative test is needed.
- `REJECT`: hypothesis contradicted or repeatedly unsupported.
- `MERGE`: combine with another hypothesis because evidence indicates the mechanisms are not separable.

Never delete REJECT rows.
