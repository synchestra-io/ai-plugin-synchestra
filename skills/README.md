# Skills

Synchestra skills teach AI agents how to use the `synchestra` CLI. One skill per CLI resource, with per-verb instructions loaded on demand via the `references/` subdirectory.

See the [agent-skills feature spec](https://github.com/synchestra-io/synchestra/blob/main/spec/features/agent-skills/README.md) for design principles and the full skill format. The structural decisions are recorded in [ADR-0002](https://github.com/synchestra-io/synchestra/blob/main/spec/decisions/0002-progressive-disclosure-skills.md), [ADR-0003](https://github.com/synchestra-io/synchestra/blob/main/spec/decisions/0003-skill-naming-plugin-namespace.md), and [ADR-0005](https://github.com/synchestra-io/synchestra/blob/main/spec/decisions/0005-user-invocable-visibility.md).

## How Skills Transform Agent Workflows

### An LSP for Specifications

What [LSP](https://microsoft.github.io/language-server-protocol/) did for code navigation, Synchestra's `feature` commands do for specification navigation. LSP gives IDEs structured access to code — symbols, definitions, references, diagnostics. Synchestra's CLI gives AI agents (and humans) structured access to specifications — features, dependencies, sections, lifecycle status.

| LSP concept | Synchestra equivalent |
|---|---|
| `textDocument/documentSymbol` | `feature info` (section TOC with line ranges) |
| `textDocument/definition` | `feature deps` (go to dependency) |
| `textDocument/references` | `feature refs` (find all referrers) |
| `workspace/symbol` | `feature list` / `feature tree` |
| Hover | `feature info` metadata (status, oq, children) |
| Call hierarchy | `--transitive` flag (follow chains) |
| Inlay hints | `--fields` flag (inline metadata) |
| Type hierarchy | `feature tree --direction up\|down` |

The difference: LSP serves IDEs via a persistent server and binary protocol. Synchestra serves AI agents via a stateless CLI and YAML output. But the semantic layer is the same — structured navigation over a domain-specific document tree.

### The Problem: Specification Navigation is Expensive

When AI agents work on spec repos, they glob, view, and grep files one by one. Each file costs tokens. Understanding "what exists" across dozens of features can consume 10,000+ tokens before the agent does any real work.

Concrete pain points:

- **Feature discovery** — reading the feature index, then individual READMEs, just to answer "what depends on what?"
- **Dependency traversal** — following `depends-on` links requires recursive file reads, each costing ~500–3,000 tokens
- **Feature creation** — editing 3+ files (README, parent index, feature index), with agents missing steps ~30% of the time
- **Context budget pressure** — agents that spend tokens on navigation have fewer tokens left for reasoning

### How Skills Solve This

- **Token efficiency** — `feature info` returns ~500 tokens of structured metadata vs. reading a 3,000-token README.
- **Structural safety** — mutation commands (`feature new`, `task new`) enforce spec conventions.
- **Progressive disclosure** — three tiers of loading: frontmatter description (always), SKILL.md body (on invoke), per-verb reference (on Read).
- **Composable enrichment** — `--fields` and `--transitive` flags let agents request exactly the metadata they need.

### Token Cost Comparison

| Operation | Without skills | With skills | Savings |
|---|---|---|---|
| List all features | ~4,000 tokens | ~500 tokens | 87% |
| Feature metadata + sections | ~3,000 | ~500 (`feature info`) | 83% |
| Transitive deps | ~9,000 (recursive reads) | ~300 (`deps --transitive`) | 97% |
| Full feature context | ~15,000 (multi-file reads) | ~2,000 | 87% |

## Available Skills

Each skill is a resource-level index; the detailed per-verb instructions live in `references/`. Skills are invoked as `/synchestra-cli:<skill-name>` (Claude Code auto-prefixes with the plugin name).

| Skill | `/` menu visible? | CLI surface wrapped | Verb count |
|---|---|---|---|
| [`task/`](task/SKILL.md) | ✅ yes | `synchestra task …` | 14 verbs |
| [`feature/`](feature/SKILL.md) | ✅ yes | `synchestra feature …` | 6 verbs |
| [`whats-next/`](whats-next/SKILL.md) | ✅ yes | `synchestra whats-next` | standalone |
| [`project/`](project/SKILL.md) | ❌ hidden | `synchestra project …` | 2 verbs |
| [`spec/`](spec/SKILL.md) | ❌ hidden | `synchestra spec …` | 2 verbs |
| [`code/`](code/SKILL.md) | ❌ hidden | `synchestra code …` | 1 verb |

Skills marked **hidden** have `user-invocable: false` — they are removed from Claude Code's `/` slash menu but Claude still auto-invokes them based on their descriptions. See [ADR-0005](https://github.com/synchestra-io/synchestra/blob/main/spec/decisions/0005-user-invocable-visibility.md) for the classification rule.

## Skill file format

Each resource skill follows this layout:

```
<resource>/
  SKILL.md         ← index table mapping user intent → reference file
  references/
    <verb>.md      ← full instructions for one CLI invocation
    ...
```

`SKILL.md` frontmatter carries three fields:

```yaml
---
name: <resource>              # matches directory name, lowercase + hyphens only
description: <one-sentence routing hint>
user-invocable: true | false  # ADR-0005 classification
---
```

`SKILL.md` body is a thin index: one or two paragraphs of context plus a table mapping user intent (e.g., "reserve a queued task for yourself") to the correct reference file. Per-verb detail lives in the reference file.

See the [agent-skills feature spec](https://github.com/synchestra-io/synchestra/blob/main/spec/features/agent-skills/README.md) for the full structural contract.

## Distribution

Install via the Synchestra.io meta-marketplace:

```
/plugin marketplace add synchestra-io/ai-marketplace
/plugin install synchestra-cli@synchestra-io
```

Requires Claude Code v2.1.110 or later if installed transitively as a dependency of another plugin (see [ADR-0004](https://github.com/synchestra-io/synchestra/blob/main/spec/decisions/0004-layered-plugin-architecture.md)).

## Competitive Context

No existing tool combines structured specification management, git-backed multi-agent coordination, and an agent-native CLI interface. GitHub Spec Kit is the closest analog — but it's flat (no hierarchy), single-user, and lacks multi-agent workflow primitives. Synchestra's skill layer gives agents a token-efficient, convention-enforcing interface that scales with spec complexity.

## Outstanding Questions

- Should Synchestra expose a proper [LSP server](https://microsoft.github.io/language-server-protocol/) for specification files? The CLI already provides the semantic layer. An LSP adapter would give humans live IDE integration: hover for feature metadata, autocomplete feature IDs, rename refactoring across specs. The Go packages powering the CLI could be reused. Tracked as a dedicated [LSP feature spec](https://github.com/synchestra-io/synchestra/blob/main/spec/features/lsp/README.md).
