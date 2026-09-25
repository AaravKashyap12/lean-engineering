# Codex behavior results — 25 September 2026

The user authorized evaluation here after Claude Code's provider failed. These are **Codex trials**, not Claude Code results. Claude preflight evidence and the unrun Claude ledger remain in [PREFLIGHT-CLAUDE-2026-09.md](PREFLIGHT-CLAUDE-2026-09.md) and [results-claude-blocked-2026-09.csv](results-claude-blocked-2026-09.csv).

## Method and limits

- One fresh trial agent and clean scratch directory per run; candidates explicitly loaded from copied repository source. No global installation was changed and expected answers were not supplied to the trial agents.
- Owners inherited the same parent model/settings; exact runtime model/effort and usage accounting were not exposed. Baselines omitted candidate instructions. Explicit loading is not an automatic-discovery test.
- Parent assessed returned answers and retained evidence, inspected code/changes, and independently reran changed Python fixtures and HTML parsing. Summaries are labeled as evaluator records; they are not passed off as raw transcript exports.
- The harness allowed four concurrent agents. Trials that could delegate had a worker slot reserved. Root-to-trial dispatch is experimental setup and is not counted as the trial owner's worker use.
- PASS means observed case acceptance; PARTIAL means correct task output but an acceptance dimension remains unverified. Requested worker model/effort is distinct from actual execution metadata. Cost, tokens, and wall-time cells remain blank where not available.
- This small, unblinded sample does not establish general quality or cost superiority. No cost-savings claim is supported.

## Recorded outcomes

8 trials: 8 PASS, 0 PARTIAL, 0 FAIL. Task-output checks passed in 8/8 runs.

| Case | Condition | Run | Status | Evidence |
| --- | --- | --- | --- | --- |
| L-a | skill | 1 | PASS | [record](evidence/codex/L-a-skill-1.md) |
| L-a | skill | 2 | PASS | [record](evidence/codex/L-a-skill-2.md) |
| L-c | skill | 1 | PASS | [record](evidence/codex/L-c-skill-1.md) |
| L-c | skill | 2 | PASS | [record](evidence/codex/L-c-skill-2.md) |
| L-e | skill | 1 | PASS | [record](evidence/codex/L-e-skill-1.md) |
| L-e | skill | 2 | PASS | [record](evidence/codex/L-e-skill-2.md) |
| L-f | skill | 1 | PASS | [record](evidence/codex/L-f-skill-1.md) |
| L-f | skill | 2 | PASS | [record](evidence/codex/L-f-skill-2.md) |

Both L-a runs recorded RED before the production fix and GREEN afterward. Independent reruns passed 9 and 8 tests respectively, with the original seven test bodies preserved. L-c correctly reported the missing verifier as a failure; L-e stayed read-only; L-f stopped before consequential actions. L-b, L-d, and L-g remain pending as requested. No comparative Lean baseline was run.
