# AGENTS.md

Universal rules for AI coding agents working in this repository.

Use this file as the small mandatory base. Keep it strict, readable, and project-agnostic. Put path-specific, framework-specific, or tool-specific details in separate files only when they are truly needed.

---

## Core Rule

Trace first. Change little. Verify.

Do not guess. Do not rewrite working code. Do not add speculative abstractions. Every changed line must map to the user request.

---

## Think Before Coding

Before editing, understand the existing implementation.

- Read the files directly related to the request.
- Trace the caller, callee, data flow, and ownership boundary.
- Search for existing helpers, constants, services, components, and patterns before creating new ones.
- State a risky or unclear assumption before acting on it.
- Ask one focused question only when ambiguity blocks safe work.

For questions, explanations, reviews, or commit text, answer the request directly. Do not inspect or edit unrelated files.

---

## Simplicity First

Use the minimum change that solves the task.

- No features beyond what was asked.
- No configurability that was not requested.
- No abstraction for single-use code.
- No broad rewrites.
- No defensive branches for impossible states.
- No new dependency unless clearly necessary.

If the solution feels clever, simplify it.

---

## Surgical Changes

Touch only files required by the task.

- Do not format unrelated files.
- Do not rename unrelated symbols.
- Do not clean unrelated dead code.
- Do not refactor nearby working code.
- Do not change public behavior unless requested.
- Remove only unused code created by your own change.

Every changed line should be easy to explain from the user request.

---

## Reuse Existing Patterns

Prefer the nearest working pattern in the repository.

Before adding new logic, search in this order:

1. Current file
2. Current folder
3. Current package or module
4. Shared utilities, constants, services, and components
5. Existing docs and rules

Avoid duplicate validation, enum lists, payload builders, permission checks, formatters, parsers, mappers, retry logic, and UI states. If duplication intentionally remains, explain why.

---

## Source of Truth

Edit the true source, not generated output.

Do not edit `dist/`, `build/`, generated files, copied mirrors, vendored code, or lockfiles unless the task requires it.

If a new rule file is needed, keep `AGENTS.md` as the base and link from it only when the split prevents unnecessary reading.

---

## Verification

Verify the smallest relevant surface before finishing.

- Run targeted tests, type checks, lint checks, or manual checks when available and reasonable.
- For bugs, trace the root cause before coding and verify the failing path.
- For UI or state changes, check loading, success, error, empty, retry, and reset states when applicable.
- If checks cannot be run, say why.

Do not claim a check passed unless it actually ran.

---

## Git Safety

Read-only git commands are allowed when useful for tracing changes.

Do not commit, push, reset, rebase, force-push, discard changes, or rewrite history unless the user explicitly asks.

Never overwrite user changes.

---

## Security

Never expose secrets.

Do not perform destructive or production-impacting actions without explicit user approval.

For irreversible actions, use clear full prose and wait for confirmation.

---

## Final Response

Be concise and concrete.

Include:

- What changed.
- Files touched.
- Checks run, or why checks were not run.
- Known risk or edge case, if any.

For bug fixes, include the root cause.

---

Small diff. Clear reason. Verified result.
