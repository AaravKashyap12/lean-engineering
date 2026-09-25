# Lean Engineering

A portable Agent Skill for focused engineering with one owning agent and real verification.

Keep the useful discipline—understand the code, reproduce the bug, test the change,
inspect the diff—without recursive reviewer swarms or unnecessary orchestration.
Works with Codex, Claude Code, and other tools that support `SKILL.md`.

## What it does

- Defines a bounded outcome before editing.
- Reads relevant repository instructions and nearby tests.
- Uses focused failing/passing checks for behavior changes where practical.
- Fixes the demonstrated cause rather than accumulating speculative patches.
- Runs relevant tests, type checks and diff inspection before claiming completion.
- Reports actual results, skipped checks and blockers without inventing success.
- Keeps one owner accountable for the plan, edits, judgment, and completion; permits evidence-returning workers within an explicit file scope.
- Excludes recursive LLM reviewers and keeps consequential work with the owner.

## Install

For Codex, available across projects:

```sh
npx skills add https://github.com/AaravKashyap12/lean-engineering --skill lean-engineering --agent codex --global
```

For Claude Code:

```sh
npx skills add https://github.com/AaravKashyap12/lean-engineering --skill lean-engineering --agent claude-code --global
```

The commands above use the third-party [Skills CLI](https://github.com/vercel-labs/skills).
The skill itself is plain Markdown and has no runtime dependencies, hooks, network
clients or executable helper scripts.

Manual installation: copy the complete `lean-engineering/` folder into the skill
directory used by your agent, for example `~/.codex/skills/lean-engineering/`.
Do not overwrite a customized existing installation without comparing it first.
Start a new task/session if your agent has not discovered the installed skill.

## Usage

```text
Use $lean-engineering to fix this bug. Reproduce it, make the smallest reliable
change, run the relevant checks, and report what passed and what remains unverified.
```

Good fits: bounded features, bug fixes, local feasibility probes and incremental
maintenance. The skill does not supply a compiler, database, simulator or credentials.
Unavailable checks must remain explicitly unverified.

## Authorization and scope

Installing a skill does not authorize production changes, deployments, secret access,
database migrations or publishing. Follow the user's task and the host's higher-level
instructions. Preserve unrelated changes and existing authorization boundaries.

## Pairing with Efficiency Skill

[Efficiency Skill](https://github.com/AaravKashyap12/efficiency-skill) helps route work
to an appropriate model tier. Lean Engineering controls the engineering workflow.

Lean governs ownership, verification, and completion. A routing skill governs the dispatch decision, model tier, and effort within those boundaries. Mechanical and recon workers may return evidence; a routing gate may also authorize a bounded implementation slice with one owner per file. Neither skill authorizes reviewer loops or consequential delegation. State the chosen mode before work.

## Repository layout

```text
lean-engineering/
  SKILL.md
  agents/openai.yaml
README.md
LICENSE
CHANGELOG.md
```

`SKILL.md` is the canonical instruction set. `agents/openai.yaml` supplies optional
Codex display metadata. The README is installation and usage documentation, not a
second competing workflow.

## Validation and limitations

The 0.2.0 revision preserves the TDD, root-cause debugging, verification ladder, and deterministic completion gate while replacing the blanket subagent ban with an owner model.

Behavior cases and the credited standard-library fixture are in [evals/README.md](evals/README.md). Results are recorded separately from package checks. No comparative improvement in code quality, costs, or production safety is established by this release. A blocked or unrun evaluation is never a pass.

## Pre-launch evaluation status

Format, protected-content, consistency, and fixture checks passed. The Codex behavior batch recorded 9/9 full passes: two runs each of L-a, L-c, L-e, and L-f, and one run of the paired case L-d with Efficiency Skill, whose cheap-tier worker model was confirmed from the Codex rollout. L-b and L-g remain pending. This is not a comparative quality/cost benchmark.

[Recorded results and limitations](evals/RESULTS-2026-09.md) · [Run ledger](evals/results-2026-09.csv). Claude Code runs remain blocked by provider failures; they are not labeled as passes.

## Contributing

Open an issue or pull request with a concrete failure case, the current behavior,
the proposed instruction change and a check that distinguishes improvement from
extra process. Keep changes small; do not add dependencies or orchestration layers
without a demonstrated need. Never include credentials or private customer data.

## License

[MIT](LICENSE). Copyright 2026 Aarav Kashyap Singh.
