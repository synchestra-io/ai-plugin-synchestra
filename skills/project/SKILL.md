---
name: project
description: Set up and configure Synchestra projects — initialize a new project (create state repo, spec repo pointer, config) and register existing repositories into a Synchestra-managed workspace. Use when bootstrapping a new Synchestra project or onboarding additional repositories.
user-invocable: false
---

# Synchestra project setup

This skill wraps the `synchestra project` command family — project initialization and configuration. Most humans run these commands once per project from a terminal; the skill exists so Claude can drive project setup conversationally when asked.

## Pick a verb

| You need to… | Read |
|---|---|
| Initialize a new Synchestra project from scratch | [references/init.md](references/init.md) |
| Set up Synchestra in an existing repository / register repositories | [references/setup.md](references/setup.md) |

## Exit codes (shared)

All `synchestra project` commands share the [Synchestra CLI exit code contract](https://github.com/synchestra-io/synchestra/blob/main/spec/features/cli/README.md#exit-code-contract). Per-verb specifics in each reference.
