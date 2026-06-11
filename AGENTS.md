# AGENTS.md

Canonical instructions for AI coding agents.

## Goal

Minimize instructions. Centralize decisions. Route domain knowledge. Track transitions explicitly.

The agent should spend its context budget learning what is unique about this project,
not relearning how to be an engineer.

## Required Context

Always read:

- `AGENTS.md`
- `PROJECT.md`

Read only the relevant file under `knowledge/` when deeper area-specific context is needed.

## Operating Rules

- Make the smallest correct change that satisfies the current request.
- Do not refactor, rename, reformat, or clean unrelated code unless requested.
- For behavior-changing code edits, trace the smallest affected path before editing.
- Skip deep tracing for docs, copy, style-only, or trivial config changes unless behavior is involved.
- Reuse existing code patterns before introducing new ones.
- Prefer consistency with the surrounding code being modified unless doing so would violate an explicit project decision.
- Do not invent APIs, data contracts, file paths, libraries, or architecture decisions.
- Do not introduce abstractions, extension points, or configuration layers unless required by the current request or already exist nearby.

## Scope Control

If the requested change reveals unrelated issues:

- Mention them briefly.
- Do not fix them unless requested.

## Escalation

Ask for clarification when:

- Multiple reasonable implementations exist and the choice affects architecture, public behavior, data contracts, or long-term maintainability.
- The task requires choosing a new architecture or dependency.
- The request conflicts with project decisions.
- The requested behavior is ambiguous and could lead to a wrong implementation.

For low-risk choices, make the smallest reasonable assumption and state it briefly.

## Context Routing

Use `PROJECT.md` for stable decisions, active transitions, known exceptions, and source-of-truth locations.

Use `knowledge/*` only for deeper domain-specific context when the task needs it.

When uncertainty may affect architecture, data contracts, shared patterns, public behavior, or migration direction, read the relevant project context first.

## Source Precedence

For implementation choices:

1. Current user request
2. This `AGENTS.md`
3. `PROJECT.md` / `knowledge/*`
4. Existing local patterns

For project facts:

1. Current codebase
2. package.json / config / schema / migrations
3. `PROJECT.md` / `knowledge/*`
4. Comments and old docs

When code and project documentation disagree, check whether the repository is in an active transition before choosing a direction.

If an active transition exists:

- Use the target direction for new work.
- Preserve legacy code unless migration is explicitly requested.
- Do not mix old and new patterns in the same changed area unless the existing boundary already does.
- Mention the transition in the final response when it affects the implementation.

If no active transition exists, follow the current code and mention the documentation mismatch.

## Project Documentation Ownership

`PROJECT.md` and `knowledge/*` should be reviewed by humans.

Agent-generated updates are suggestions until accepted.

Do not update `PROJECT.md` or `knowledge/*` unless requested, or unless the task explicitly includes maintaining project documentation.

Do not add unstable, one-off, or unreviewed patterns to project context.

## Context File Control

- Do not create new agent/context Markdown files unless requested.
- Do not split project context into new files unless the existing file is becoming too large or hard to navigate.

## Final Response For Code Changes

Include:

- files changed
- root cause, if fixing a bug
- checks run
- checks not run, if any
- notable risk
