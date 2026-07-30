# Machine-users & workers

Three related things power execution in 4PM. Getting the vocabulary right makes everything else
easier.

## The three pieces

- **Worker** — a physical or virtual machine you control. It's where the actual work happens
  (AI runs, Git runs, files live).
- **CLI** — the `4pm` command-line app installed on a worker. One worker can run **several** CLIs
  at once. Each CLI has its own profile and serves **one project**.
- **Machine-user** — a *user* in your org that represents a paired CLI. You attach a machine-user
  to a project; permissions and quota apply to it like any other user (it holds the **MACHINE**
  role).

The relationship is **1:1:1** — one CLI ↔ one machine-user ↔ one project's working copy on the
worker.

```
Worker (one machine)
├── CLI #1  ↔  machine-user A  →  Project X
├── CLI #2  ↔  machine-user B  →  Project Y
└── CLI #3  ↔  machine-user C  →  Project Z
```

## Lifecycle

1. **Pair** a CLI (see [Connect a worker](./03-connect-a-worker.md)). This creates/links a
   machine-user, which appears as **idle** in the machines area.
2. **Attach** the machine-user to a project (during project creation, or from the project's
   machine selector).
3. **Use** it — dispatch AI/Git/shell commands to that project; they run on the worker via this
   CLI.
4. **Detach / re-pair** as needed. Removing a project or re-pairing to a new CLI cleans up the
   old link.

## Where you manage them

- The **machines area** (`/machines`) lists your machine-users and their status: **idle**,
  connected/serving, or offline.
- Each machine-user has a detail view with **Info · Usage · Console · Logs · History**.
- If project creation says there's **no idle machine-user**, pair a new CLI or free one up first.

## Status you'll see

| Status | Meaning |
| --- | --- |
| **idle** | Paired and connected, but not yet serving a project. Ready to attach. |
| **connected / serving** | Actively attached to a project and available for commands. |
| **busy** | Currently running a command. |
| **offline** | The CLI isn't connected (worker off, network down, or CLI stopped). |

## Usage & metering

AI work run by a machine-user is **metered to your organization** and counts against your plan's
quota. See [Plans, billing & add-ons](./10-billing-and-plans.md) and
[Run AI agents](./06-running-ai-agents.md) for how quota and token limits apply.

Don't want to run your own worker? You can **rent a 4PM-operated machine-user** — see
[Rent a 4PM machine-user](./11-rented-machines.md).
