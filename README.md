# Synchestra AI Plugin

AI plugin for [Synchestra](https://synchestra.io) — skills that teach AI agents how to use the `synchestra` CLI for spec-driven development, task coordination, and (soon) remote work dispatch.

This repository contains the plugin source. It is installed on top of the [`synchestra` CLI](https://github.com/synchestra-io/synchestra); the CLI is a prerequisite.

## Contents

| Directory | Description |
|---|---|
| [`skills/`](skills/README.md) | Agent skills — one per `synchestra` CLI resource group, per-verb instructions progressively loaded |
| [`.claude-plugin/`](.claude-plugin/plugin.json) | Claude Code plugin manifest |

See [`skills/README.md`](skills/README.md) for the skill catalogue, design principles, and token-efficiency rationale.

## Install

Via the [Synchestra.io meta-marketplace](https://github.com/synchestra-io/ai-marketplace):

```
/plugin marketplace add synchestra-io/ai-marketplace
/plugin install synchestra-cli@synchestra-io
```

Requires Claude Code v2.1.110 or later if installed transitively as a dependency of another plugin (see [ADR-0004](https://github.com/synchestra-io/synchestra/blob/main/spec/decisions/0004-layered-plugin-architecture.md)).

## Relationship to the CLI

The plugin wraps the `synchestra` CLI — it does not replace it. Skills encode *when* to call a command, *which* flags to pass, and *how* to interpret exit codes. The CLI contract (commands, flags, exit codes) is defined in [`synchestra/spec/features/cli/`](https://github.com/synchestra-io/synchestra/tree/main/spec/features/cli).

A change in the CLI surface typically produces a matching reference update in this repository; the two evolve together but release independently.

## Relationship to other plugins

`synchestra-cli` is a **CLI wrapper plugin** in the base layer of the Synchestra.io plugin ecosystem (see [ADR-0004](https://github.com/synchestra-io/synchestra/blob/main/spec/decisions/0004-layered-plugin-architecture.md)). Sister CLI wrapper: [`specscore-cli`](https://github.com/synchestra-io/ai-plugin-specscore). The methodology plugin [`spec-driven-development`](https://github.com/synchestra-io/ai-plugin-sdd) depends on both.

## Releases

Releases are tagged as `synchestra-cli--v<version>` on this repository to support Claude Code's native plugin dependency resolution.

## License

MIT — see [LICENSE](LICENSE).

## Outstanding Questions

- Distribution channel branding (e.g., `install.synchestra.io`) — deferred pending MVP of remote dispatch.
