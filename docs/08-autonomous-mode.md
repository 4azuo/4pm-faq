# Autonomous mode

Autonomous mode lets a project **work on its own on a schedule**: the workers' CLIs wake up, turn
**approved requests** into tasks, implement **approved tasks** one by one on their own branches, and
deliver each as a **pull request** (or, if a manager allows it, merge it straight into the base branch) —
while you watch and approve from the dashboard. Nothing runs until a person approves it.

You drive it all from the web; there's nothing to install on the worker (no cron).

## Where to find it

Project › **Content** › **AI content** › **Autonomous**, with three sub-tabs:

- **Overview** — **Start all / Pause all** for the project, the **Workers** table (each worker's switch,
  teams, state, AI profile, **Last check**, current task, failures) and **Tasks in progress** (tasks and
  the requests being taken in, with stale claims flagged), tasks waiting to be split, and warnings.
- **Settings** — **Project settings** (shared by every worker) and **Worker settings** (one worker), as a
  form or JSON.
- **Logs** — up to 7 days at once, filtered by date range, type, ID or text; click an ID to see only its
  lines.

A worker runs cycles only when the project switch, 4PM's permission and its own switch are all on.
Starting/pausing needs the project's **autonomous** permission (ADMIN/PM by default). You can also stop or
start a worker's autonomous mode from Home › Machines › Machine users.

Next to it, AI content › **Flow** shows every request as one lane — request, docs, tasks and questions up
to done — coloured by state; click a step to open its row.

### Last check

The Workers table's **Last check** says what the last cycle did (e.g. *Intake: 3 task(s), 1 question(s)*,
*Finished TSK-…*) or why it waited: quiet hours, daily tick limit, AI usage limit, project folder busy,
paused on a question, unapproved, conflict with the base branch, the plan's monthly book limit, or a reason
the worker is **not allowed** (project switch off, project paused / closed / not created yet, folder not
provisioned, not a member). When nothing can run it lists what waits for you.

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
   **data-model (ER) change** or a **system-diagram change**. New tasks are **Pending** — they need
   approval. A request is taken in by one worker only.
   - **Docs step** (when the spec declares doc types and *Docs step before implement* is on): the request
     first gets a **DOC** row; the AI writes its docs, you review each round in **Review docs** and choose
     **Proceed** or **Revise**, and its tasks start only from the accepted docs.
3. **Claims** the next eligible task — approved, dependencies done, not over its attempt limit — so two
   workers never take the same task.
4. **Implements** it on its own branch (`dev/<base>/<group>/<task>`), committing as it goes. A task that
   continues earlier work first takes in the newest base branch (and again before delivery); the AI
   resolves conflicts on the way.
5. **Delivers** it: pushes the branch and opens a **pull request** into the base branch (for each
   touched submodule too, then a root PR that links them) — or merges it directly when *Merge without a
   pull request* is on. The task moves to **AI Done** with the PR links.

What happens when a task doesn't finish:

- **Needs a decision** → the AI asks a question in User Q&A, the task waits on it, and resumes once
  the answer is approved.
- **Out of AI quota** → work is saved and the task resumes when quota returns.
- **Failed or timed out** → work is pushed to the task branch (no PR), the task goes back to AI Todo
  and an attempt is counted. A timed-out run that **made progress** doesn't count toward the automatic
  pause.
- **Too many attempts** (5 by default) → the AI proposes **smaller tasks** that need your approval; the
  original moves to AI Done as "split into …".
- **Conflict with base** the AI can't resolve → the task stops; fix the conflict, then press **Retry**.
- **Unapproved while running** → the run stops; the work stays on the branch and continues after
  re-approval.

By default you review and **merge the PRs yourself**. 4PM never approves rows; it merges or deletes branches
only when an ADMIN / PM turned on *Merge without a pull request* or *Daily branch cleanup*.

## The books branch & protecting your base branch

The books are kept on a separate branch, **`autonomous-books/<base>`**, which follows your base branch.
With the default settings autonomous code arrives through pull requests, so you can (and should)
**protect** the base branch and require PRs. (File saves from the web's file screens and *Merge without a
pull request* do write to the base branch — they need the workers to be allowed to push there.)

The one thing you must **not** protect is `autonomous-books/<base>`: the workers need to push the books
there. If it's protected, the cycle stops and the Overview shows a warning.

## Settings

Settings are split into **Worker settings** (per worker) and **Project settings** (shared by all workers).
Every setting, its default and when to change it: [Autonomous settings explained](../faq/autonomous-settings.md).

| Setting | Scope | What it does |
| --- | --- | --- |
| **Schedule** | worker | When ticks run (default every 10 minutes): presets or a custom cron; mistakes are flagged and the next run times shown. |
| **Quiet hours** | worker | A From/To window (worker's local time) when no tick runs. |
| **Max ticks per day** | worker | Upper bound on runs per day (−1 = unlimited). |
| **Stop after N failures** | worker | Pause automatically after N failed runs in a row (3; 0 = off). |
| **Max session / weekly %** | worker | Skip a run when the AI account's 5-hour session (80 %) or weekly (90 %) usage is at the cap (checked per AI profile; skipped only if every profile is over). |
| **Log retention** | worker | Days to keep the run logs (14). |
| **Agent run timeout** | project | Max minutes for one AI run (60). |
| **Claim timeout / claim check** | project | How long a task claim lasts (6 h) and how often it's re-checked (10 min). |
| **Max attempts** | project | Attempts before a task is split (5). |
| **Task size hints** | project | What sizes S and M mean (S 5 files / 300 lines, M 20 / 1 500); larger tasks are split at intake. |
| **Evidence / mockup / ER / sequence / system-diagram folders** | project | Where those files go in the repo (default under `.4pm/`). |
| **Auto-approve system-diagram changes** | project | Apply diagram change requests at once (on). |
| **Auto-approve ER changes** | project | Apply ER change requests at once (off). |
| **Docs step before implement** | project | Write and review a request's docs before its tasks (on; needs doc types in the spec). |
| **Merge without a pull request** | project, ADMIN/PM | Merge finished tasks straight into the base branch (off; falls back to a PR). |
| **AI resolves conflicting PRs** | project | Each cycle fixes one conflicting 4PM task PR (off). |
| **Daily branch cleanup** + **after (days)** | project, ADMIN/PM | Delete dead 4PM task branches once a day (off; 14 days; restorable). |

The project's Settings tab also holds **Send every change through autonomous** (on by default): while the
project is ready, Console runs, AI generate and Git writes are refused and changes are posted as requests.

Each run uses the **model of the worker's AI profile** — there's no separate autonomous model.

## Several workers & teams

- Several workers can serve the same project: each claims different tasks.
- In **Members › AI routing** you can choose which **teams** each worker serves; a restricted worker then
  takes only requests and tasks of those teams. See
  [Worker pools & AI routing](./24-worker-pools-and-routing.md).

## Safety guards

- While autonomous is **running**, disruptive actions on that worker — re-syncing/re-cloning the repo,
  updating the CLI — are refused; pause autonomous first. "Update all CLIs" skips such workers.
- While a cycle works in a project folder, Console prompts and Git changes on that worker wait their turn.
  Uncommitted changes found in the folder are stashed (`git stash`) and you're notified with the stash
  name.
- Worker restarts and CLI updates wait for running work to finish (the worker shows **Restarting**).
- Pausing the project stops its autonomous work (claims are kept) and resuming starts it again.
- Approvals are **signed** by 4PM: a row that changed after approval, or an approval not made through
  4PM, doesn't count until re-approved.
- If an AI run tries to change the approval or authorship records, the change is undone and the
  project managers are notified.
- Only the MCP servers and network hosts you approved are reachable from AI runs (see
  [Project content](./25-project-content.md#networks)).

## Plan limits

Each plan caps the **new rows per book per month** (User Todo, User Q&A, AI Todo — Free 300, Pro 1 000,
Max 5 000). At the cap, new requests wait (managers are notified, and Last check says so) but approved
tasks are still implemented. A full hosted
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
