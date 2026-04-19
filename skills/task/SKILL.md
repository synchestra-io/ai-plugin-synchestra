---
name: task
description: Manage Synchestra tasks across their full lifecycle — pick work, claim, track progress, report status, block, unblock, complete, fail, abort, list, create. Use whenever you need to read or change a task's state.
user-invocable: true
---

# Synchestra task management

This skill wraps the `synchestra task` command family. Pick the verb that matches your current need and read the corresponding reference for full instructions, parameters, and exit codes.

## Pick a verb

| You need to… | Read |
|---|---|
| Reserve a queued task for yourself | [references/claim.md](references/claim.md) |
| Begin work on a claimed task | [references/start.md](references/start.md) |
| Report progress or heartbeat on an in-progress task | [references/status.md](references/status.md) |
| Mark a task done successfully | [references/complete.md](references/complete.md) |
| Mark a task failed with a reason | [references/fail.md](references/fail.md) |
| Release a claim back to the queue | [references/release.md](references/release.md) |
| Request an in-progress task be aborted | [references/abort.md](references/abort.md) |
| Transition a task to the `aborted` terminal state | [references/aborted.md](references/aborted.md) |
| Mark a task blocked on a dependency | [references/block.md](references/block.md) |
| Unblock a blocked task and put it back in progress | [references/unblock.md](references/unblock.md) |
| Move a `planning` task to the `queued` state | [references/enqueue.md](references/enqueue.md) |
| Create a new task | [references/new.md](references/new.md) |
| Inspect details of one task | [references/info.md](references/info.md) |
| List available or filtered tasks | [references/list.md](references/list.md) |

## Exit codes (shared)

All `synchestra task` commands share the [Synchestra CLI exit code contract](https://github.com/synchestra-io/synchestra/blob/main/spec/features/cli/README.md#exit-code-contract). Each reference documents verb-specific exit codes on top of the shared contract.
