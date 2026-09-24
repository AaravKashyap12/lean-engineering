---
name: lean-engineering
description: "Use for efficient single-agent engineering with real checks."
license: MIT
metadata:
  version: 0.1.0
  author: Aarav, Hermes Agent
  platforms: [linux, macos, windows]
  hermes:
    tags: [single-agent, engineering, tdd, verification, efficiency]
    related_skills: [test-driven-development, systematic-debugging, plan]
---

# Lean Engineering

Deliver reliable software changes with one continuous agent session. Preserve planning, TDD, root-cause debugging, and evidence-based completion; remove recursive subagent, reviewer, and re-review loops.

## When to Use

- Building or modifying software when speed and token efficiency matter.
- Executing a defined plan or a bounded change in an existing repository.
- Debugging a defect with reproducible local checks.

Do not use this skill for destructive external actions, production deployment, security-sensitive changes, migrations, or changes whose correctness cannot be tested locally without first getting the user's explicit direction.

## Non-Negotiable Execution Mode

- Work in one continuous agent session.
- Do not dispatch subagents, parallel agents, LLM reviewer agents, or re-review loops.
- Do not invoke `subagent-driven-development`, `dispatching-parallel-agents`, `requesting-code-review`, or `receiving-code-review` unless the user explicitly asks for that exception in the current task.
- Prefer local deterministic checks over language-model judgment.
- Never claim a check passed without running and inspecting it.

If another installed workflow recommends a swarm, this skill governs the execution mode for this task because the user chose lean single-agent engineering.

## Procedure

1. **Classify the work.**
   - For a quick feasibility question, state the probe and keep outputs throwaway.
   - For a bounded code change, state the intended behavior, touched area, and verification command in 2-5 lines.
   - For a multi-file or architectural change, write a compact plan: goal, constraints, task order, changed files, and checks.
   - Completion criterion: scope, acceptance behavior, and validation command are explicit before editing.

2. **Inspect only relevant context.**
   - Read the local instructions, target code, analogous code, and the nearest existing tests.
   - Establish the narrowest useful test/type/lint commands before changing production code.
   - Completion criterion: the next edit and the command that can disprove it are known.

3. **Implement vertically with TDD.**
   - For each behavior change: write one focused failing test, run it and confirm the expected failure, implement the smallest change, then rerun the focused test.
   - Run the relevant regression command after each completed behavior slice.
   - For configuration, generated code, or throwaway spikes where test-first is inappropriate, say why and use the strongest applicable deterministic check.
   - Completion criterion: each behavior has direct evidence, not only a final broad test run.

4. **Debug by evidence.**
   - When a check fails unexpectedly, reproduce it, inspect the failure and relevant code path, state the root-cause hypothesis, then make the smallest test-backed fix.
   - Do not make speculative batches of fixes.
   - Completion criterion: the reproduction no longer fails and the regression test remains in place when appropriate.

5. **Perform a deterministic completion gate.**
   - Run the project-appropriate test suite or the broadest feasible relevant subset.
   - Run applicable type checking, linting, formatting validation, build, or static analysis.
   - Inspect `git diff --check`, `git diff --stat`, and the changed-file diff; account for every changed file and remove unrelated changes.
   - Report commands, exit outcomes, any skipped checks, and why a skipped check could not run.
   - Completion criterion: all claimed checks have fresh evidence; scope is intentional and no known failure is hidden.

## Verification Ladder

Use the highest checks the repository supports, in this order where applicable:

1. Focused regression test for the behavior changed.
2. Relevant package/module test suite.
3. Type checker, linter, formatter validation, and build.
4. Full repository test suite when feasible.
5. Diff hygiene: `git diff --check`, `git diff --stat`, and manual changed-file inspection.

A green linter is not a replacement for a behavioral test. A passing test suite is not a replacement for inspecting scope.

## Escalation

Stay single-agent by default. Pause and ask the user before proceeding when work involves:

- irreversible external actions, deployment, merges, pushes, or publication;
- secrets, authentication, authorization, payments, personally identifiable data, or security boundaries;
- database/data migrations, destructive file operations, or production data;
- concurrency/distributed consistency where the available checks cannot establish confidence.

Propose the narrowest additional check or review needed. Do not create a reviewer swarm.

## Pitfalls

- Do not replace testing with a self-authored prose review.
- Do not turn one failed check into several speculative edits.
- Do not use a full suite as an excuse to skip the focused RED-GREEN evidence.
- Do not create a long plan for a bounded edit; the plan must reduce uncertainty, not become ceremony.
- Do not delete an installed third-party skill library to control behavior. Keep it intact for updates and override the execution policy with this skill or project instructions.

## Completion Report

Report only:

- what changed;
- verification commands and actual results;
- skipped checks and blockers, if any;
- the next decision required from the user, if any.

Do not report success if a named acceptance check did not run or failed.
