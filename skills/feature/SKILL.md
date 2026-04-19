---
name: feature
description: Navigate and manage Synchestra feature specifications — list features, render hierarchy trees, inspect metadata, trace dependencies, find reverse references, create new features. Use whenever you need to understand or change the spec graph.
user-invocable: true
---

# Synchestra feature navigation

This skill wraps the `synchestra feature` command family — Synchestra's "LSP for specifications." Pick the verb that matches your current need.

## Pick a verb

| You need to… | Read |
|---|---|
| List features in the project (flat view) | [references/list.md](references/list.md) |
| Render the feature hierarchy as a tree | [references/tree.md](references/tree.md) |
| Inspect one feature's metadata, sections, and children | [references/info.md](references/info.md) |
| Trace what a feature depends on | [references/deps.md](references/deps.md) |
| Find what depends on (references) a feature | [references/refs.md](references/refs.md) |
| Create a new feature | [references/new.md](references/new.md) |

## Exit codes (shared)

All `synchestra feature` commands share the [Synchestra CLI exit code contract](https://github.com/synchestra-io/synchestra/blob/main/spec/features/cli/README.md#exit-code-contract). Per-verb specifics in each reference.
