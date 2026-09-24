# Lean Engineering

A portable Agent Skill for focused, single-agent engineering with real verification.

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
- Defaults to one agent; multi-agent execution requires an explicit user exception.

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

Their defaults differ: Lean uses one agent; Efficiency can delegate. When using both,
keep the single-agent default unless the user explicitly permits delegation for the
current task. After that exception, Efficiency may route bounded subtasks; Lean's
testing, scope and evidence requirements still apply. State the chosen mode before work.

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

The initial release preserves the author's existing local v0.1 skill instructions.
Package validation checks names/frontmatter, metadata and source-copy integrity.
It does not prove better code quality, lower token cost, production safety or a
particular benchmark result. No comparative behavior evaluation has been published.
Stars or installation counts are not a substitute for reviewing instructions.

## Contributing

Open an issue or pull request with a concrete failure case, the current behavior,
the proposed instruction change and a check that distinguishes improvement from
extra process. Keep changes small; do not add dependencies or orchestration layers
without a demonstrated need. Never include credentials or private customer data.

## License

[MIT](LICENSE). Copyright 2026 Aarav Kashyap Singh.
