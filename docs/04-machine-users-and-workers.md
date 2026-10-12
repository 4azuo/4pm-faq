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

> **Orchestrator CLI.** A root/ADMIN can also pair a CLI to **their own account** (leave the
> machine-user empty when pairing). That *orchestrator* CLI doesn't serve a project; it identifies the
> machine and can run short AI requests outside a project (such as spec suggest/review). Its connection
> shows in Settings and in the Machines list.

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
- The **Machine users** list shows each worker's **CLI version** (amber = update available, red = too old
  to connect), the **AI accounts** it uses, the pools it belongs to, and its last error. **Update all
  CLIs** updates every online worker that's behind (skipping autonomous, rented and locked-image
  workers).
- **Machines** also has **Workers**, **Pools** ([Worker pools & AI routing](./24-worker-pools-and-routing.md)),
  **Links**, **Configs** ([Worker configuration](./21-worker-config.md)) and **Tools** (copy tools between
  machines).
- A worker's page shows live **metrics** (CPU, memory, disk, IO pressure, swap, OOM, processes).

## A machine-user's page

Besides **Info · Usage · Console · Commands · Memory · Tools · Logs · History**, managers (and the worker
account itself) can set, per machine-user:

- **Worker configs** — the CLI's config (see [Worker configuration](./21-worker-config.md));
- **Usage limits** — a quota-token and command limit per period across all its connections (0 = no
  limit);
- **Usage alerts** — email a designated address when its AI usage crosses a threshold;
- **Data retention** — how many days the CLI keeps its logs, command history and output (capped by your
  plan);
- **Worker network** — the worker's observed network posture (outbound open or restricted, inbound).
  4PM only observes it; sandbox the host or container yourself (or use project
  [Networks](./25-project-content.md#networks) rules);
- **SSH deploy key** (rented workers) — generate a key on the worker and add its public key as a Deploy Key
  on your repo, for private repos without a GitHub App / GitLab credential;
- **Language** of the worker's messages, and the sign-in **IP allowlist**.

A worker account's role is fixed (MACHINE) and can't be given management permissions.

## Status you'll see

| Status | Meaning |
| --- | --- |
| **idle** | Paired and connected, but not yet serving a project. Ready to attach. |
| **connected / serving** | Actively attached to a project and available for commands. |
| **busy** | Currently running a command. |
| **offline** | The CLI isn't connected (worker off, network down, or CLI stopped). |
| **not provisioned** | Attached to a project, but the repo couldn't be cloned (often git authentication) — fix it and **Retry**. |

## Usage & metering

AI work run by a machine-user is **metered to your organization** and counts against your plan's
quota. See [Plans, billing & add-ons](./10-billing-and-plans.md) and
[Run AI agents](./06-running-ai-agents.md) for how quota and token limits apply.

Don't want to run your own worker? You can **rent a 4PM-operated machine-user** — see
[Rent a 4PM machine-user](./11-rented-machines.md).
