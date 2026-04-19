---
name: spec
description: Validate and search Synchestra specification repositories — lint against structural conventions and search specs with spec-aware scoping. Use when a user asks to check spec hygiene or find content across spec features.
user-invocable: false
---

# Synchestra specification tooling

This skill wraps the `synchestra spec` command family — spec validation and search. Typical invocations: pre-commit spec linting and conversational spec search.

## Pick a verb

| You need to… | Read |
|---|---|
| Lint a spec repository against structural conventions | [references/lint.md](references/lint.md) |
| Search specs for a keyword with spec-aware scoping | [references/search.md](references/search.md) |

## Exit codes (shared)

All `synchestra spec` commands share the [Synchestra CLI exit code contract](https://github.com/synchestra-io/synchestra/blob/main/spec/features/cli/README.md#exit-code-contract). Per-verb specifics in each reference.
