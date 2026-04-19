---
name: code
description: Query source-code relationships to Synchestra resources — find which source files reference which features (synchestra source-reference annotations). Use when you need impact analysis or want to know "what code implements this feature?"
user-invocable: false
---

# Synchestra code-to-spec navigation

This skill wraps the `synchestra code` command family. Where `feature` navigates the spec → spec graph, `code` navigates the code → spec graph — surfacing source files that reference features via Synchestra source-reference annotations.

## Pick a verb

| You need to… | Read |
|---|---|
| List source files that depend on a feature | [references/deps.md](references/deps.md) |

## Exit codes (shared)

`synchestra code` commands share the [Synchestra CLI exit code contract](https://github.com/synchestra-io/synchestra/blob/main/spec/features/cli/README.md#exit-code-contract). Per-verb specifics in [references/deps.md](references/deps.md).
