# Workers & pairing

**What is a "worker"?**
A machine you control that runs the `4pm` CLI and does the actual work (AI, Git, shell). See
[docs/04](../docs/04-machine-users-and-workers.md).

**How do I connect a worker?**
Install the `4pm` CLI on it and pair it with your account using a 1 → 2 → 3 hashcode handshake:
run the CLI to get hashcode (1), enter it on the web to get (2), enter (2) in the CLI to confirm,
and the server returns (3) which the CLI saves. Full steps:
[docs/03](../docs/03-connect-a-worker.md).

**What's a machine-user vs. a CLI vs. a worker?**
- **Worker** — the machine.
- **CLI** — the `4pm` app on it (one worker can run several).
- **Machine-user** — the *user* in your org that represents a paired CLI; you attach it to a
  project. It's 1 CLI ↔ 1 machine-user ↔ 1 project. See
  [docs/04](../docs/04-machine-users-and-workers.md).

**Can one machine run several projects?**
Yes — run several CLIs on the same worker; each has its own machine-user and serves one project.

**How do I install the CLI?**
With **Node ≥ 24**: `npm i -g @4pm/cli`, then `4pm --version`. No npm? Use the release tarball or
Docker. The in-app `/cli` page has copy-paste commands for each OS. Full steps:
[docs/15](../docs/15-install-cli.md).

**Do agents run in a sandbox? Can I run the CLI in Docker / headless?**
You can install the CLI **directly** on the host, or run it as a **Docker container** where the
container itself is the **sandbox** isolating the agent from the host (pull
`ghcr.io/4azuo/4pm-cli:full`, pair once, sign in with `4pm ai-login`, run detached). Either way it
runs **headless** (observed from the web Console), with an optional **TUI** you attach via
`4pm attach`. See [docs/15](../docs/15-install-cli.md#option-2--docker-headless).

**My hashcode was rejected.**
Hashcodes are short-lived. Restart pairing and enter them promptly.

**The CLI won't connect after pairing.**
Check the worker's network/firewall and that the CLI is up to date (it auto-updates on startup).

**My old CLI suddenly logged out.**
Expected if the same machine-user was paired to a **different** CLI — a machine-user links to
exactly one CLI (1:1), so the old certificate is revoked.

**How do I move a project's worker to a new machine?**
Re-pair its machine-user on the new machine. The old link is revoked automatically.

**What status does a paired machine show?**
`idle` (paired, not yet on a project), connected/serving, `busy`, or `offline`. See them in the
machines area (`/machines`).

**Do I need my own worker at all?**
No — you can **rent** a 4PM-operated machine-user instead
([docs/11](../docs/11-rented-machines.md)).

**My worker's CLI version is shown in red or amber.**
Amber = a newer CLI is available. Red = too old: the server will refuse it the next time it connects —
update it (`4pm update`, the **Update** button, or pull a newer Docker image).

**A machine shows "Not provisioned".**
It was attached to a project but couldn't clone the repo — usually git authentication. Fix it in the
project's **Git › Configuration**, then **Retry**.

**How do I restart a worker?**
Machines › Machine users › **Restart** on its row. The CLI restarts once its running job finishes, so no
work is lost; a **Restarting** tag shows next to its CLI version meanwhile, and new commands are told to
resend later.

**How do I stop a worker's autonomous mode before updating it?**
Use **Stop / Start autonomous** on its row in Machine users — no need to open the project. To stop every
worker at once (e.g. before **Update all CLIs**), use **Stop all autonomous** above the table. Each worker's
switch is set; start them again per row, or per project with **Start all workers** in Autonomous.

**Which workers are running AI right now, on which account?**
A live **Running / Idle** status shows on the user page, the project header, the Console and the autonomous
Workers table (AI profile column); Machine users marks the AI account in use.

**How are AI accounts shared between workers?**
AI runs spread over the AI accounts your workers share: an idle account is used first, and an account that
reaches its usage limit is skipped by every worker until it resets. AI Help, Research, checklist drafting
and shared memory fail over between accounts too (including Codex and API-key accounts).

**How do I update every worker at once?**
**Machines › Machine users › Update all CLIs**. Workers in autonomous mode, rented workers and
locked-image workers are skipped and named.
