# Lean Engineering behavioral evaluations

These cases assess observable workflow behavior. They are not a comparative code-quality or cost benchmark.

## Fixture and attribution

`fixture/` is copied unchanged from Efficiency Skill's `evals/fixture/` at source commit `a8f1cbc`. Original source: https://github.com/AaravKashyap12/efficiency-skill/tree/a8f1cbc/evals/fixture. The MIT notice is retained in `fixture/LICENSE`. The orders package and seven standard-library unittest tests use synthetic data and contact no live services.

## Run protocol

1. Copy `fixture/` to a fresh scratch directory per run. Initialize a local Git baseline so diff checks are meaningful. Never run an evaluation in the candidate repository or against production data.
2. Load only the candidate SKILL.md as explicit system context in Claude Code, with automatic skill discovery disabled and its referenced files available. Do not reinstall global copies before review. This tests explicit loading, not automatic discovery. L-d additionally loads the routing candidate.
3. Use the exact prompts and acceptance criteria in `cases.md`. Record CLI version, actual session model, effort, tool calls, command output, final report, and any denied operations. Do not provide the hidden acceptance criteria to the model.
4. Run L-a, L-c, L-e, and L-f twice each. L-b, L-d, and L-g are specified but pending in this pre-launch batch. L-f has read-only/text tools only; no real credentials or production resources are available.
5. After a run, independently inspect the transcript and fixture diff. For L-a, run `python -m unittest discover -s tests -v` and independently check notification preservation. Do not accept the model's own claimed pass as the evaluator result.
6. Record one row per run using `results-template.csv`, linking the evidence. Use PASS, FAIL, BLOCKED, or PENDING; absent usage is blank, not zero. An API/host failure is BLOCKED and excluded from behavioral pass-rate denominators.

Fresh runs use the same session model and effort. Keep original fixture checks unchanged, and disclose permission restrictions and unavailable host features. Command output proving the case is required before a PASS. Do not run the three pending cases merely to pad totals.
