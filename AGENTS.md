# AGENTS.md

Universal rules for AI coding agents working in this repository.

Use this file as the small mandatory base. Keep it short, strict, and project-agnostic. Put long, rare, path-specific, or tool-specific details in separate markdown files and link to them.

---

## Core Rule

Trace first. Change little. Verify. Reply terse.

Do not guess. Do not rewrite working code. Do not add speculative abstractions. Every changed line must map to the user request.

---

## Operating Mode

Be concise but technically exact.

* Remove filler.
* Keep important context.
* Preserve exact code, paths, commands, API names, errors, and numbers.
* Use normal clear prose when safety, destructive actions, migrations, or multi-step instructions could be misunderstood.
* Prefer direct answers over long explanations.

---

## Mandatory Pre-Edit Gate

Before editing code, verify:

* Related files found.
* Caller and callee read.
* Current data flow traced.
* Existing helper/component/hook/util/service/constant searched.
* Nearby implementation pattern checked.
* Minimal required change understood.
* Risky or unclear assumption stated.

If any item is not done, do not edit yet.

---

## Task Triage

Before working, classify the task:

* **Question/explanation**: answer only. Do not inspect or edit unrelated files.
* **Bug fix**: reproduce or trace root cause before coding.
* **Feature**: identify smallest vertical change from UI/API/data flow.
* **Refactor**: only do requested scope. Preserve behavior.
* **Docs**: update source docs only. Do not invent commands or behavior.
* **Review comment**: verify claim before applying.
* **Commit/PR text**: output text only unless user explicitly asks for git commands.

Ask one focused question only when ambiguity blocks safe work. Otherwise proceed with stated assumptions.

---

## Simplicity First

Use the minimum code that solves the task.

Do not add:

* Features not requested.
* Configurability not requested.
* Abstractions for one use.
* Broad rewrites.
* Defensive branches for impossible states.
* New dependencies unless clearly necessary.

If a solution feels clever, simplify it.

---

## Surgical Change Rule

Touch only files required by the task.

Do not:

* Format unrelated files.
* Rename unrelated symbols.
* Clean unrelated dead code.
* Refactor nearby working code.
* Change public behavior unless requested.

Remove only unused code created by your own change.

---

## Reuse Before Create

Before adding any helper, validator, mapper, formatter, enum list, API payload builder, or UI state handler, search first.

Search order:

1. Current file
2. Current folder
3. Current package/module utils
4. Shared/common utils
5. Shared components
6. Constants/enums
7. Service/API layer
8. Existing docs/rules

If equivalent logic exists, reuse or extend it. Do not create parallel logic.

---

## No Duplicate Logic

Avoid duplicate:

* Validation regex
* Enum/type membership list
* API payload assembly
* Permission checks
* Formatter/parser/converter
* Mapping/classification switch
* Error/loading/empty-state UI
* Retry/reset behavior

If duplication intentionally remains, explain where, why, and risk.

---

## Follow Existing Patterns

Match the closest existing pattern.

Check:

* File structure
* Naming
* Imports
* State management
* Component style
* API service style
* Error handling
* Loading/empty/success states
* Translation/localization
* Test style
* Logging style

If multiple patterns exist, follow the nearest one in the same package/module.

---

## UI and Component Rules

Keep UI code readable.

* No complex inline functions inside JSX/template props.
* No validation logic inside components if reusable.
* No direct API calls from components when service layer exists.
* No raw user-facing text when translation/i18n exists.
* Keep loading, error, empty, success, retry, and reset states consistent.
* Preserve user input on errors unless product behavior says otherwise.

Trivial one-line handlers are acceptable.

---

## API and Data Flow Rules

Use existing service/API layers.

When adding or changing API behavior:

* Reuse existing HTTP helpers.
* Reuse base URL/path constants.
* Match nearby request/response handling.
* Reuse payload builders when available.
* Keep discriminator logic near enums/types.
* Prefer explicit `type`, `kind`, or `category` fields over guessing from incidental data shape.
* Ask for or inspect real request/response samples if contract is unclear.

Do not hardcode API paths, payload shapes, or magic strings when a source of truth exists.

---

## Bug Fix Rules

For bugs, identify root cause before coding.

Trace:

* Where data is created.
* Where it is transformed.
* Where it is stored.
* Where it is sent.
* Where success/error is handled.
* Where UI resets or closes.
* Where retry or partial success happens.

Fix the source, not only the visible symptom.

---

## Batch / Partial Success Rules

For batch operations:

* Progress reflects actual completed work.
* Successful items stay completed.
* Failed items remain identifiable and recoverable.
* User input and failed data are preserved for retry.
* Error messages must not hide partial success.
* Retry/reset behavior must be clear.

Do not clear all input because one item failed.

---

## State Safety

Check all relevant states before finishing:

* Initial
* Loading
* Success
* Error
* Empty
* Retry
* Reset
* Partial success
* Disabled/readonly
* Permission denied, if applicable

Do not only test the happy path.

---

## Source of Truth Rule

Before editing a file, check whether it is source or generated.

Do not edit:

* `dist/`
* `build/`
* generated files
* copied/synced mirrors
* lockfiles unless dependency change requires it
* vendored code unless explicitly requested

Edit the true source file. If unsure, search for generation/sync notes.

---

## Markdown / Rule File Split

`AGENTS.md` is the mandatory base. Keep it small enough to read every session.

Do not create new `.md` files just for neatness.

Create a separate markdown file only when:

* Content is too long for the base file.
* Rule is path-specific, framework-specific, tool-specific, or rarely needed.
* The separate file prevents agents from reading unnecessary details for unrelated tasks.
* `AGENTS.md` keeps a short summary and pointer to the file.

Preferred generic location:

```text
docs/ai-rules/<topic>.md
```

Optional tool-specific wrappers only when the project intentionally uses that tool:

```text
CLAUDE.md                  # Claude wrapper, usually points to AGENTS.md
.cursor/rules/*.md         # Cursor-specific scoped rules
.github/copilot-instructions.md
.claude/rules/*.md         # Claude-specific detailed rules
```

If a new `.md` file is created, final response must explain:

* Why existing docs could not be reused.
* When the file should be read.
* Which base rule points to it.

Do not split tiny content into separate files.

---

## Documentation Rules

Docs are product artifacts.

When editing docs:

* Be accurate.
* Use clear language.
* Keep setup commands runnable.
* Keep feature lists synced with code.
* Do not invent benchmark numbers, limits, or behavior.
* Preserve existing product voice if intentional.
* Update docs when behavior changes.

README is the front door. Treat it like UI copy.

---

## Tests and Verification

Run existing targeted checks when available and reasonable.

Prefer:

* Existing unit tests for changed module.
* Existing integration tests for changed flow.
* Existing lint/typecheck for touched package.
* Manual test checklist when automated tests are absent.

Do not add new test files unless user asks or repo convention clearly expects tests for this change.

If checks cannot be run, say why.

---

## Security and Destructive Actions

Never expose or commit secrets.

Do not perform destructive actions without explicit user approval:

* Delete data.
* Drop database/table/column.
* Force push.
* Reset branch.
* Remove migrations.
* Delete files outside task scope.
* Run production-impacting commands.

For irreversible actions, use clear full prose. No compressed wording.

---

## Review Comment Rules

AI/bot review comments are hypotheses.

Before applying:

* Trace the claim.
* Check if failure is reachable.
* Check existing patterns.
* Reject changes that add dead guards, duplicate logic, or broad rewrites.

Human reviewer comments should usually be followed when feasible, simpler, and consistent with the codebase.

If rejecting a comment, explain the specific reason and risk.

---

## Git Rules

Do not run git commands unless explicitly asked.

When asked for commit message, output only text.

Commit format:

```text
<type>: <scope-or-ticket>: <short result>
```

Allowed common types:

```text
feat, fix, chore, docs, style, test, build, ci, perf, refactor
```

Prefer describing user-visible result, not implementation steps.

---

## Final Self-Check

Before final response after code changes, verify:

* Related flow traced.
* Minimal change made.
* Duplicate logic searched.
* Existing patterns reused.
* No unrelated refactor.
* No unnecessary new file.
* No complex inline JSX/template logic.
* Validation/check logic placed correctly.
* API/service layer respected.
* UI states checked.
* User input/error behavior preserved.
* Source of truth edited.
* Generated files avoided.
* Tests/checks run or reason provided.

If any item fails, fix before responding.

---

## Required Final Response After Code Changes

Use this format:

```md
Changed:
- <short summary>

Files:
- <changed file 1>
- <changed file 2>

Self-check:
- Flow traced: yes
- Minimal change: yes
- Duplicate logic checked: yes
- Existing patterns reused: yes
- Unrelated refactor avoided: yes
- New files necessary: yes/no
- UI states checked: yes/not applicable
- API/service layer checked: yes/not applicable
- Tests/checks: <command/result or not run + reason>
- Existing behavior preserved: yes

Risk / edge case:
- <risk, edge case, or "None found">
```

For bug fixes, add:

```md
Root cause:
- <why it was broken>
```

If any self-check item is `no`, explain why.

---

## Final Reminder

Small diff. Clear reason. Verified result.

If unsure, trace more. If still unsure, ask one precise question.
