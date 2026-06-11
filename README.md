# strict-agents-md

A minimal instruction framework for AI coding agents.

Store decisions, not advice. Route context, do not preload it.

## Why This Exists

AI coding agents often fail in predictable ways:

- editing before tracing
- rewriting working code
- duplicating existing helpers
- adding speculative abstractions
- skipping verification

`strict-agents-md` keeps agent instructions short and moves project-specific decisions into `PROJECT.md`. The goal is to avoid generic context files that make agents over-explore while still giving them the stable decisions they cannot infer safely.

## Quick Start

Copy [`AGENTS.md`](AGENTS.md) and [`PROJECT.md`](PROJECT.md) into the root of your project:

```sh
curl -o AGENTS.md https://raw.githubusercontent.com/ttat288/strict-agents-md/main/AGENTS.md
curl -o PROJECT.md https://raw.githubusercontent.com/ttat288/strict-agents-md/main/PROJECT.md
```

Then edit `PROJECT.md` by hand with the stable decisions that are unique to your project.

For tool-specific setup, copy `AGENTS.md` and `PROJECT.md` first, then copy the matching wrapper into the same project:

| Tool | Wrapper |
| --- | --- |
| Claude Code | [`examples/claude/CLAUDE.md`](examples/claude/CLAUDE.md) |
| Cursor | [`examples/cursor/.cursor/rules/base.mdc`](examples/cursor/.cursor/rules/base.mdc) |
| GitHub Copilot | [`examples/copilot/.github/copilot-instructions.md`](examples/copilot/.github/copilot-instructions.md) |

Wrappers are intentionally small. They should point the tool back to the root `AGENTS.md`; they should not duplicate or replace the base rules.

## File Roles

- `AGENTS.md`: how the agent should work.
- `PROJECT.md`: stable project decisions, active transitions, exceptions, and source-of-truth locations.
- `knowledge/*`: optional deeper domain context for large projects.

## What It Enforces

- Make the smallest useful change.
- Read stable project decisions before guessing.
- Route deeper context only when the task needs it.
- Prefer current code over stale documentation.
- Prefer explicit project decisions over local habits.
- Keep wrappers thin.

## Design Principles

- Keep the base files short enough to read every session.
- Keep tool wrappers thin.
- Put project-specific decisions in `PROJECT.md`.
- Split extra rules only when they prevent agents from reading unrelated details.
- Prefer decisions over generic advice.

## Examples

- [`examples/minimal`](examples/minimal): the smallest useful setup.
- [`examples/claude`](examples/claude): Claude Code wrapper.
- [`examples/cursor`](examples/cursor): Cursor rules wrapper.
- [`examples/copilot`](examples/copilot): GitHub Copilot instructions wrapper.

## Philosophy

Minimize instructions. Centralize decisions. Route domain knowledge. Track transitions explicitly.

## License

MIT.
