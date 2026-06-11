# strict-agents-md

A small, strict, project-agnostic `AGENTS.md` template for AI coding agents.

Copy one file. Make AI code safer.

## Use It

Copy [`AGENTS.md`](AGENTS.md) into the root of your project.

For tool-specific setup, copy the matching wrapper:

| Tool | Wrapper |
| --- | --- |
| Claude Code | [`examples/claude/CLAUDE.md`](examples/claude/CLAUDE.md) |
| Cursor | [`examples/cursor/.cursor/rules/base.mdc`](examples/cursor/.cursor/rules/base.mdc) |
| GitHub Copilot | [`examples/copilot/.github/copilot-instructions.md`](examples/copilot/.github/copilot-instructions.md) |

## What It Enforces

- Trace before editing.
- Make the smallest required change.
- Reuse existing patterns.
- Avoid duplicate logic.
- Verify before the final response.

## Philosophy

Small diff. Clear reason. Verified result.

## License

MIT.
