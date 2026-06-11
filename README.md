# strict-agents-md

A minimal project-governance framework for coding agents.

A minimal instruction framework that teaches coding agents what makes your project different.

## Why This Exists

This is not a prompt pack.
This is a small project-governance layer for AI coding agents.

Most coding agents already know software engineering. What they usually lack is project-specific context:

- architectural decisions already made
- shared patterns the team intentionally uses
- legacy areas that should not be touched
- migrations currently in progress
- deliberate exceptions
- source-of-truth locations

`strict-agents-md` keeps agent behavior in `AGENTS.md`, stable project decisions in `PROJECT.md`, and optional deeper context in `knowledge/*`.

The goal is to help coding agents preserve project decisions, reduce architectural drift, and avoid loading unrelated context.

## Quick Start

Copy [`AGENTS.md`](AGENTS.md) and [`PROJECT.md`](PROJECT.md) into the root of your project:

```sh
curl -o AGENTS.md https://raw.githubusercontent.com/ttat288/strict-agents-md/main/AGENTS.md
curl -o PROJECT.md https://raw.githubusercontent.com/ttat288/strict-agents-md/main/PROJECT.md
```

Then edit `PROJECT.md` by hand with the stable decisions that are unique to your project.

For a small repo, this is usually enough:

```txt
/
|-- AGENTS.md
`-- PROJECT.md
```

For a larger repo, add `knowledge/` only when stable domain context becomes too detailed for `PROJECT.md`:

```txt
/
|-- AGENTS.md
|-- PROJECT.md
`-- knowledge/
```

Agents should read `knowledge/*` only when the current task needs that deeper context.

For tool-specific setup, copy `AGENTS.md` and `PROJECT.md` first, then copy the matching wrapper into the same project:

| Tool | Wrapper |
| --- | --- |
| Claude Code | [`examples/claude/CLAUDE.md`](examples/claude/CLAUDE.md) |
| Cursor | [`examples/cursor/.cursor/rules/base.mdc`](examples/cursor/.cursor/rules/base.mdc) |
| GitHub Copilot | [`examples/copilot/.github/copilot-instructions.md`](examples/copilot/.github/copilot-instructions.md) |
| Codex-compatible agents | root [`AGENTS.md`](AGENTS.md) |

Wrappers are intentionally small. They should point the tool back to the root `AGENTS.md`; they should not duplicate or replace the base rules.

## File Roles

- `AGENTS.md`: how the agent should work.
- `PROJECT.md`: stable project decisions, active transitions, exceptions, and source-of-truth locations.
- `knowledge/*`: optional deeper domain context for large projects.

Current code defines reality. `Active Transitions` define the future direction.

## Why Decisions Matter

Generic advice like "think carefully" competes for context without telling the agent what is unique about the project.

Project decisions are more useful because they are specific:

- which API client is canonical
- which legacy path should stay untouched
- which migration target new work should follow
- which schema, config, or route file is the source of truth
- which exceptions are intentional

## Small Repos

Use only `AGENTS.md` and `PROJECT.md`.

Keep `PROJECT.md` short enough to review by hand. Put stable choices there, not temporary notes or task-specific findings.

## Large Repos

Keep `AGENTS.md` as the behavior router.

Use `PROJECT.md` for stable decisions, active transitions, known exceptions, and source-of-truth locations.

Add `knowledge/*` only for deeper domain-specific context that agents should read selectively. Do not preload every area of the system into every session.

## Tool Wrappers

Claude Code, Cursor, and GitHub Copilot can use their own instruction files, but those files should stay thin:

```md
Use the repository instructions in `AGENTS.md`.
```

For Codex-compatible agents, place `AGENTS.md` at the repository root.

## Examples

- [`examples/minimal`](examples/minimal): the smallest useful setup.
- [`examples/claude`](examples/claude): Claude Code wrapper.
- [`examples/cursor`](examples/cursor): Cursor rules wrapper.
- [`examples/copilot`](examples/copilot): GitHub Copilot instructions wrapper.

## Philosophy

Minimize instructions. Centralize decisions. Route domain knowledge. Track transitions explicitly.

Teach the agent the project, not software engineering.

## License

MIT.
