# strict-agents-md

A small, strict, project-agnostic `AGENTS.md` template for AI coding agents.

Copy one file. Make AI code safer.

## Why This Exists

AI coding agents often fail in predictable ways:

- editing before tracing
- rewriting working code
- duplicating existing helpers
- adding speculative abstractions
- skipping verification

`strict-agents-md` is a strict base template that pushes agents toward small, traceable, verified diffs. It is not a replacement for project-specific instructions; it is the base layer you copy first.

## Quick Start

Copy [`AGENTS.md`](AGENTS.md) into the root of your project:

```sh
curl -o AGENTS.md https://raw.githubusercontent.com/ttat288/strict-agents-md/main/AGENTS.md
```

Or copy it manually from this repository.

For tool-specific setup, copy `AGENTS.md` first, then copy the matching wrapper into the same project:

| Tool | Wrapper |
| --- | --- |
| Claude Code | [`examples/claude/CLAUDE.md`](examples/claude/CLAUDE.md) |
| Cursor | [`examples/cursor/.cursor/rules/base.mdc`](examples/cursor/.cursor/rules/base.mdc) |
| GitHub Copilot | [`examples/copilot/.github/copilot-instructions.md`](examples/copilot/.github/copilot-instructions.md) |

Wrappers are intentionally small. They should point the tool back to the root `AGENTS.md`; they should not duplicate or replace the base rules.

## What It Enforces

- Trace before editing.
- Make the smallest useful change.
- Reuse existing patterns.
- Avoid duplicate logic.
- Verify before responding.
- Keep git actions explicit.

## Design Principles

- Keep the base file short enough to read every session.
- Keep tool wrappers thin.
- Put project-specific details in the project that uses the template.
- Split extra rules only when they prevent agents from reading unrelated details.
- Prefer clear rules over exhaustive policy.

## Examples

- [`examples/minimal`](examples/minimal): the smallest useful setup.
- [`examples/claude`](examples/claude): Claude Code wrapper.
- [`examples/cursor`](examples/cursor): Cursor rules wrapper.
- [`examples/copilot`](examples/copilot): GitHub Copilot instructions wrapper.

## Philosophy

Small diff. Clear reason. Verified result.

## License

MIT.
