# Autonomous settings explained

Where: Project › Content › AI content › **Autonomous** › **Settings** (Form or JSON). The settings come in two
panels:

- **Project settings (all workers)** — shared by every worker of the project: claims, attempts, run timeout,
  task size, repo folders, approvals of diagrams, how tasks are delivered, docs step, branch cleanup.
- **Worker settings** — one worker at a time: schedule, quiet hours, ticks per day, failure stop, log
  retention and AI-usage caps. Pick the worker from the Workers table (⚙ **Settings of this worker**).

Changing them needs the project's **autonomous** permission (ADMIN / PM by default). A few switches are
**ADMIN or the project's PM only** — marked below. See also [Autonomous mode](./autonomous-mode.md) and
[docs/08](../docs/08-autonomous-mode.md#settings).

## Worker settings (per worker)

| Setting | Default | What it means | When to change it |
| --- | --- | --- | --- |
| **Paused** | On (for a new worker) | The worker's own switch. When on, this worker starts no cycle — same as Pause in its row. | Use the Start / Pause buttons instead; they do the same. |
| **Cron schedule** | `*/10 * * * *` (every 10 min) | When this worker wakes up to run a cycle ("tick"). Standard 5-field cron, run by the 4PM CLI itself — nothing to install on the machine. The form shows the next run times and flags mistakes. | Slower (`0 * * * *` hourly) to save AI quota; faster for a busy project. |
| **Quiet hours** | Off | A From–To window (worker's local time) when no cycle starts. An overnight window like 22:00–07:00 works. | Keep the AI quiet while people review, or to save quota for daytime Console work. |
| **Max ticks / day** | −1 (unlimited) | Upper bound on cycles that actually run per day. | Cap a costly project. |
| **Stop after N failures** | 3 | After N failed cycles in a row the worker **auto-pauses** itself and managers are notified (0 = never). Timeouts that made progress don't count. | Raise it if your tasks often need a retry; lower it to stop sooner. |
| **Log retention (days)** | 14 | Per-day run logs older than this are deleted (0 = keep forever). | Keep longer for audits. |
| **Max session %** | 80 | Skip a cycle when the AI account's **5-hour session** usage is at or above this %. Checked per AI profile — skipped only when every profile is over. | Lower it to keep room for people using the Console. |
| **Max weekly %** | 90 | Same, for the **7-day** usage. | Lower it near the end of a busy week. |

## Project settings (all workers)

### Claims, attempts & time limits

| Setting | Default | What it means |
| --- | --- | --- |
| **Claim timeout (hours)** | 6 | A worker "claims" the task it works on so no other worker takes it. A claim older than this may be **taken over** by another worker, and a task that ran out of AI quota goes back to AI Todo. |
| **Claim check (minutes)** | 10 | How often a running task re-checks that its worker still holds the claim. A lost claim stops the run (its work is kept on the branch). |
| **Max attempts per task** | 5 | After this many failed attempts the AI **splits** the task into smaller tasks — they need your approval. |
| **Agent run timeout (minutes)** | 60 | Longest time one AI run (intake, implementation, split, docs) may take. The work so far is saved and continued next time. Between 5 minutes and the claim timeout. Raise it for big tasks. |
| **Size S / Size M — files, changed lines** | S: 5 files / 300 lines · M: 20 files / 1 500 lines | **Hints** for the analysis when it sizes tasks (the "Size S / M" badge in AI Todo). Not hard limits: anything bigger is sized **L** and split at intake. |

### Repo folders

Where autonomous writes its files in the repo (repo-relative path such as `.4pm/evidence`; letters, digits,
`. _ -`; no `..`, not inside `.git`). Files written before a change keep working.

| Folder | Default | Holds |
| --- | --- | --- |
| **Evidence folder** | `.4pm/evidence` | Files attached to book rows and the AI's proof of work. |
| **Mockup folder** | `.4pm/mockups` | UI mockups drawn at intake (one HTML file per screen). |
| **ER folder** | `.4pm/er` | The project data model (one file per module) and its change requests — on the books branch. |
| **Sequence folder** | `.4pm/sequences` | Sequence diagrams of tasks and questions. |
| **System-diagram folder** | `.4pm/diagrams` | The draw.io system diagram and its change requests — on the books branch. |

### Approvals of models

| Setting | Default | What it means |
| --- | --- | --- |
| **Auto-approve system-diagram changes** | **On** | A new or revised system-diagram change request is applied as soon as it is saved. Off: it waits for someone with the diagram-approve permission — and the tasks of its group wait too ("Diagram pending"). |
| **Auto-approve ER changes** | **Off** | Same for the data model (ER). Off: ER changes wait for an approver, and their tasks wait. Turn it on only if you trust the AI's schema changes. |

### Docs step

| Setting | Default | What it means |
| --- | --- | --- |
| **Docs step before implement** | On (only acts when the spec declares doc types) | After intake, each request gets a **DOC** row: the AI writes the request's docs first (at least an ADR when your project keeps ADRs), you review each round and choose **Proceed** or **Revise**, and the request's tasks start only from the accepted docs. Turn it off to go straight from request to tasks. |

### Delivering tasks

| Setting | Default | Who can change | What it means |
| --- | --- | --- | --- |
| **Merge without a pull request** | Off | ADMIN / PM only | A finished task is merged (merge commit) **straight into the base branch** instead of opening a PR. If the merge fails, a PR is opened instead. ⚠ No review and no CI before code lands; the base branch must accept the workers' pushes; undo a task with `git revert -m 1 <merge commit>`. The worker table shows a **Direct merge** badge. |
| **AI resolves conflicting PRs** | Off | autonomous permission | Each cycle, before new work, the AI resolves **one** conflicting pull request of a 4PM task branch and pushes the fix. Each PR state is tried once; a failure notifies the managers. |

### Branch cleanup

| Setting | Default | Who can change | What it means |
| --- | --- | --- | --- |
| **Daily branch cleanup** | Off | ADMIN / PM only | Once a day, delete the **4PM task branches** that are merged, whose PR is closed or whose task is gone. Other branches are never deleted automatically. Every deletion is logged and restorable in **Git › Branch cleanup**. |
| **Clean up after (days)** | 14 | ADMIN / PM only | Only branches with no commit for this many days are cleaned up. |

## The project-level switch: "Send every change through autonomous"

This one lives in the project's **Settings** tab (panel **Autonomous path**), not in the Autonomous screen.
**On by default.** While the project is ready (created or linked):

- the **Console**, **AI generate** and **Git writes** are refused — changes are posted as **requests** in
  User Todo instead (the **AI request** button on file screens does that for you);
- saving files in Files / Reports / Tests / Subagents / Skills / CLAUDE.md still works and **commits to the
  base branch**.

Turn it off to allow direct runs again; direct actions then warn you when workers run autonomous on the
project (with **Pause all** and **Send via autonomous**). A project that isn't created yet is not affected.

## Common questions

**Which settings apply to one worker and which to all?**
Schedule, quiet hours, ticks per day, failure stop, log retention and the usage caps are **per worker**.
Everything else is **per project**.

**What is a safe setup to start with?**
Keep the defaults: PRs on (Merge without a PR off), ER auto-approve off, docs step on, daily cleanup off.
Approve a few tasks and watch one cycle in **Logs** before approving more.

**I want the AI to work only at night.**
Set quiet hours to the working day (e.g. 08:00–19:00) on each worker, or use a cron such as
`*/15 0-6 * * *`.

**Tasks keep timing out.**
Raise **Agent run timeout** (it can't exceed the claim timeout — raise that too if needed), or lower the
**Size** hints so the analysis makes smaller tasks.

**Why is "Merge without a pull request" greyed out?**
Only an ADMIN or the project's PM can change it (same for daily branch cleanup).

**Can I edit the settings as JSON?**
Yes — switch **Form / JSON**. Invalid values are refused with the field that's wrong.
