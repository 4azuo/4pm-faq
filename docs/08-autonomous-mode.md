# Autonomous mode

Autonomous mode lets a project **work on its own on a schedule**: the worker's CLI wakes up, turns
**approved requests** into tasks, implements **approved tasks** one by one on their own branches, and
delivers each as a **pull request** — while you watch and approve from the dashboard. Nothing runs
until a person approves it, and nothing is merged for you.

You drive it all from the web; there's nothing to install on the worker (no cron).

## Where to find it

Project › **Content** › **AI content** › **Autonomous**, with three sub-tabs:

- **Overview** — the **Start / Pause** switch, the Running/Paused badge, the tasks in progress (one per
  worker, with stale claims flagged), tasks waiting to be split, and warnings.
- **Settings** — the schedule and limits (form or JSON).
- **Logs** — the run logs by date.

Starting/pausing needs the project's **autonomous** permission (ADMIN/PM by default).

## The task books

The work lives in **books** — tables stored in the project repo:

| Book | Holds | Written by |
| --- | --- | --- |
| **User Todo** | Requests from people (`REQ-…`) | Team members and customers |
| **User Q&A** | The AI's questions (`QA-…`) — you answer them | The AI asks; people answer |
| **AI Todo** | Tasks to implement (`TSK-…`) | The AI (from requests) and people |
| **AI Done** | Read-only history of finished tasks, with PR links and evidence | The AI |

Every request, question and task must be **approved** before the AI acts on it. How to write,
approve and discuss rows: [Task books & approvals](./28-task-books-and-approvals.md).

## How a cycle runs

On each scheduled run (a "tick"), the worker:

1. **Syncs** the books branch (see below) with the latest base branch.
2. **Intake** — if there are approved requests or answered questions, the AI analyses them and writes
   new **tasks** into AI Todo (and new **questions** into User Q&A when it needs a decision). For UI
   requests it also draws an **HTML mockup**; it can draw a **sequence diagram** per task and propose a
   **data-model (ER) change**. New tasks are **Pending** — they need approval.
3. **Claims** the next eligible task — approved, dependencies done, not over its attempt limit — so two
   workers never take the same task.
4. **Implements** it on its own branch (`dev/<base>/<group>/<task>`), committing as it goes.
5. **Delivers** it: pushes the branch and opens a **pull request** into the base branch (for each
   touched submodule too, then a root PR that links them). The task moves to **AI Done** with the PR
   links.

What happens when a task doesn't finish:

- **Needs a decision** → the AI asks a question in User Q&A, the task waits on it, and resumes once
  the answer is approved.
- **Out of AI quota** → work is saved and the task resumes when quota returns.
- **Failed or timed out** → work is pushed to the task branch (no PR), the task goes back to AI Todo
  and an attempt is counted. A timed-out run that **made progress** doesn't count toward the automatic
  pause.
- **Too many attempts** (5 by default) → the AI proposes **smaller tasks** that need your approval; the
  original moves to AI Done as "split into …".

You review and **merge the PRs yourself** — 4PM never merges, approves rows or deletes branches on its
own.

## The books branch & protecting your base branch

The books are kept on a separate branch, **`autonomous-books/<base>`**, which follows your base branch.
4PM **never pushes to the base branch** — all code arrives through pull requests — so you can (and
should) **protect** the base branch and require PRs.

The one thing you must **not** protect is `autonomous-books/<base>`: the workers need to push the books
there. If it's protected, the cycle stops and the Overview shows a warning.

## Settings

| Setting | What it does |
| --- | --- |
| **Schedule** | When ticks run: presets (every N minutes/hours, daily, Mon–Fri at a time) or a custom cron. Mistakes are flagged as you type, and you see the next run times. |
| **Quiet hours** | A From/To window when no tick runs. |
| **Max ticks per day** | Upper bound on runs per day. |
| **Stop on consecutive failures** | Pause automatically after N failed runs in a row. |
| **Session / weekly usage caps** | Skip a run when the AI account's 5-hour session or weekly usage is near its limit (checked per AI profile; it skips only if every profile is over). |
| **Agent run timeout** | Max minutes for one AI run (default **60**). |
| **Claim timeout / claim check** | How long a task claim lasts (6 h) and how often it's re-checked (10 min). |
| **Max attempts** | Attempts before a task is split (5). |
| **Task size hints** | What "small" and "medium" mean for this project; large tasks are always split at intake. |
| **Evidence / mockup / ER / sequence folders** | Where those files go in the repo (default under `.4pm/`). |
| **Log retention** | Days to keep the run logs. |

Each run uses the **model of the worker's AI profile** — there's no separate autonomous model.

## Several workers & teams

- Several workers can serve the same project: each claims different tasks.
- In **Members › AI routing** you can choose which **teams** each worker serves; a restricted worker then
  takes only requests and tasks of those teams. See
  [Worker pools & AI routing](./24-worker-pools-and-routing.md).

## Safety guards

- While autonomous is **running**, disruptive actions on that worker — re-syncing/re-cloning the repo,
  updating the CLI — are refused; pause autonomous first. "Update all CLIs" skips such workers.
- Approvals are **signed** by 4PM: a row that changed after approval, or an approval not made through
  4PM, doesn't count until re-approved.
- If an AI run tries to change the approval or authorship records, the change is undone and the
  project managers are notified.
- Only the MCP servers and network hosts you approved are reachable from AI runs (see
  [Project content](./25-project-content.md#networks)).

## Plan limits

Each plan caps the **new rows per book per month** (User Todo, User Q&A, AI Todo — Free 300, Pro 1 000,
Max 5 000). At the cap, the AI stops adding rows but still implements approved tasks. A full hosted
storage also pauses new runs.

## Notifications

Project managers are notified (in-app, at most once a day per problem) when the books branch is
protected, a task was taken over, a task hit its attempt limit or was split, or a task is waiting for an
answer. You can also react to these events with [automation rules](./27-automation-rules.md).

## Tips

- Start with a few approved tasks and watch one cycle in the **Logs** before approving more.
- Use **dependencies** and **groups** to sequence work instead of approving everything at once.
- Protect the base branch, leave `autonomous-books/<base>` unprotected.
- If a task didn't run, check: is it approved (no "changed after approval" badge)? Are its dependencies
  done and its questions answered? Is autonomous paused, in quiet hours, or over a usage cap? Is the
  worker online?

See also: [Autonomous mode FAQ](../faq/autonomous-mode.md) ·
[Task books & approvals](./28-task-books-and-approvals.md).
