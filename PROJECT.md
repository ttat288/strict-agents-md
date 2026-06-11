# PROJECT.md

Stable project decisions. Keep this file small.

Status: active
Last reviewed: 2026-06-11

## Core Decisions

- This repository publishes a minimal AI-agent instruction framework.
- `AGENTS.md` defines how agents work.
- `PROJECT.md` holds stable project decisions, active transitions, exceptions, and source-of-truth locations.
- Tool-specific wrappers should stay thin and route agents back to the root `AGENTS.md`.
- Domain or area-specific details belong under `knowledge/` only when the project is large enough to need them.

## Active Transitions

- Reposition from a universal advice template toward a decision-routing framework.

## Known Exceptions

- Example wrapper files may contain tool-specific front matter when required by the tool.

## Source Of Truth

- Base agent instructions: `AGENTS.md`
- Stable project decisions: `PROJECT.md`
- Usage guidance: `README.md`
- Tool wrappers: `examples/*`
- Release notes: `CHANGELOG.md`
- Line-ending rules: `.gitattributes`

## Additional Context

No `knowledge/` files exist yet.

Add `knowledge/` only when stable, reviewed context becomes too detailed for this file.
