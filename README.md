# Synchestra AI Plugin

AI plugin for [Synchestra](https://synchestra.io) — skills that teach AI agents how to use the `synchestra` CLI for spec-driven development, task coordination, and (soon) remote work dispatch.

This repository contains the plugin source. It is installed on top of the [`synchestra` CLI](https://github.com/synchestra-io/synchestra); the CLI is a prerequisite.

## Contents

| Directory | Description |
|---|---|
| [`skills/`](skills/README.md) | Agent skills — one per `synchestra` CLI command, token-efficient, progressively loaded |
| [`.claude-plugin/`](.claude-plugin/plugin.json) | Claude Code plugin manifest |

See [`skills/README.md`](skills/README.md) for the full skill catalogue, design principles, and token-efficiency rationale.

## Install

Planned install path via the CLI:

```bash
synchestra skill install
```

This downloads the latest plugin release matching the installed CLI version.

## Relationship to the CLI

The plugin wraps the `synchestra` CLI — it does not replace it. Skills encode *when* to call a command, *which* flags to pass, and *how* to interpret exit codes. The CLI contract (commands, flags, exit codes) is defined in [`synchestra/spec/features/cli/`](https://github.com/synchestra-io/synchestra/tree/main/spec/features/cli).

A change in the CLI surface typically produces a matching skill update in this repository; the two evolve together but release independently.

## License

Apache 2.0 — see [LICENSE](LICENSE).

## Outstanding Questions

- Skill naming / prefix convention across plugins — tracked in the parent [Synchestra](https://github.com/synchestra-io/synchestra) project.
- Distribution channel branding (e.g., `install.synchestra.io`) — deferred pending MVP of remote dispatch.
