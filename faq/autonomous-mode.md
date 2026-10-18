# Autonomous mode

**What is autonomous mode?**
It lets a project **work on its own on a schedule**: the workers turn approved requests into tasks,
implement approved tasks on their own branches and deliver each one — as a **pull request** by default —
while you watch and approve from the dashboard. See [docs/08](../docs/08-autonomous-mode.md).

**How do I turn it on/off?**
Project › Content › AI content › **Autonomous** › Overview:
- **Start all / Pause all** switches the whole project (every worker).
- Each row of the **Workers** table has its own Start / Pause.
- A worker runs cycles only when the project switch, 4PM's permission and its own switch are all on.

You can also stop or start a worker's autonomous mode from **Home › Machines › Machine users** — handy before
updating its CLI. There's nothing to install on the worker (no cron).

**What do the columns of the Workers table mean?**
- **Teams** — which teams' work the worker takes (set in Members › AI routing).
- **State** — Running, Waiting, Paused, Auto-paused (after repeated failures), Offline, Restarting,
  Suspended (project paused), Not ready (project not created yet), Not allowed…
- **AI profile** — the AI account it uses now.
- **Last check** — what the last cycle did or why it waited (see below).
- **Task** — what it is doing right now: *Intake REQ-…*, a task, *Writing docs*, *Delivering*.
- **Failures** — failed cycles in a row.

**What does "Last check" tell me?**
What the last cycle did — e.g. *Intake: 3 task(s), 1 question(s)*, *Finished TSK-…* — or why it didn't work:
*Quiet hours*, *Daily tick limit reached*, *AI usage limit reached*, *Project folder busy*, *Task paused on a
question*, *Stopped: the task was unapproved*, *Stopped: the task conflicts with the base branch*,
*new requests wait: this month's limit is reached*, or a reason it is **not allowed** (project switch off,
project paused or closed, the worker's folder not provisioned yet, the worker not a member…). When nothing
can run it lists what **waits for you**: rows to approve, ER change requests, answers, dependencies.

**What are the autonomous settings and what do they do?**
See [Autonomous settings explained](./autonomous-settings.md) — every setting, its default and when to
change it.

**Does the AI run tasks without my say-so?**
No. Requests, questions and tasks all need **approval** in the books (User Todo, User Q&A, AI Todo) before
the AI acts on them. Tasks the AI writes start **Pending**. See
[Task books & approvals](./task-books-and-approvals.md).

**Does it merge code into my main branch?**
By default no — each task arrives as a **pull request** into the base branch; you review and merge it.
An ADMIN or the PM can turn on **Merge without a pull request**: finished tasks are then merged straight
into the base branch (with no review or CI first; a PR is opened if the merge fails).

**What is the "docs step" / the DOC rows in AI Todo?**
When the project spec declares doc types, every approved request first gets a **DOC** row: the AI writes
the request's documents (an ADR at least, if you keep ADRs). Open **Review docs** on the row: you see each
doc file as a diff against the base, files that other open requests also change, and earlier rounds. Write
your opinion and choose **Proceed** (docs accepted, the tasks may start from them) or **Revise** (the AI runs
another round with your opinion). Turn it off with **Docs step before implement** in Settings.

**How do I see where each request is?**
AI content › **Flow**: every request as one lane — request → docs → tasks and questions → done — coloured
by state. Click a step to open its row; a step with discussions shows how many are open.

**A task says "Conflict with base".**
Tasks that continue earlier work take in the newest base branch first and again just before delivery, and
the AI resolves conflicts on the way. If it can't, the task stops with **Conflict with base**: resolve the
conflict on the task branch (Git tab), then press **Retry** on the task.

**My PR has conflicts — can the AI fix them?**
Yes: Git › Pull requests › **Resolve with AI**. Or turn on **AI resolves conflicting PRs** in the
autonomous settings so each cycle fixes one conflicting 4PM task PR on its own.

**What is the `autonomous-books/<base>` branch?**
Where the books and approval records live. It follows your base branch. **Don't protect it** — workers
must push to it; if it's protected, runs stop with a warning.

**I approved a task but it didn't run.** Check **Last check** first, then that:
- it's still approved (no **Changed after approval** / **Unsigned** badge);
- its **dependencies** are done (two or more dependencies must have their PRs **merged**) and its
  linked questions are answered and approved;
- its group's **ER change** / **system-diagram change** is approved (badge *Diagram pending*), its **docs**
  are accepted, and its linked **discussions** are resolved;
- autonomous isn't **paused**, in **quiet hours**, over **max ticks per day** or over the **usage caps**;
- the worker is **online** and serves the task's **team**.
Then read the run **Logs** (filter by date range, type, ID or text; click an ID to see only its lines).

**I unapproved a task while the AI was running it.**
The run stops when you save. The work so far stays on the task branch and continues once you approve the
task again.

**A run stopped part-way through a task.**
Each AI run has a time limit (**Agent run timeout**, 60 minutes by default). The work is pushed to the
task's branch and the task goes back to AI Todo to resume. Raise the timeout in Settings for big tasks.

**Autonomous paused itself.**
A worker pauses after several failed cycles in a row (**Stop after N failures**, 3 by default) and you're
notified. Check the Logs, fix the cause, then press Start. Timeouts that made progress don't count.

**A task was "split into …".**
It failed its maximum attempts (5 by default), so the AI proposed smaller tasks. Approve the new tasks
to continue.

**The AI asked a question in User Q&A.**
The task needs a decision. Answer it (and approve the answer); the task resumes on the next run.

**Can I make it run now instead of waiting for the schedule?**
Yes, through the public API: `POST /v1/projects/{id}/autonomous/run` runs one cycle right away. Paused mode
and quiet hours still apply. See [Public API](../docs/32-public-api.md#run-autonomous-mode-now).

**Which AI model does it use?**
The model of the worker's AI profile. There's no separate autonomous model setting.

**Can several workers work on one project?**
Yes. Each claims a different task or request, so they never run the same one — a request is taken in by
one worker only (*Request already being taken in by …*). You can limit a worker to certain **teams** in
Members › AI routing.

**Why can't I use the Console / AI generate / Git writes on my project?**
The project has **Send every change through autonomous** on (the default): changes go in as requests.
Use the **AI request** button on a file screen, or post in User Todo. A manager can turn it off in the
project's Settings › Autonomous path.

**I saved a file in Files / CLAUDE.md while autonomous runs — is that safe?**
Yes. The save commits straight to the base branch; tasks in progress pick it up when they next update.
You're told if someone changed the file since you opened it.

**My Console prompt says it is waiting for the autonomous cycle.**
While a cycle works in the project's folder on that worker, Console prompts and Git changes there wait
their turn; the notice says which task is running.

**I was notified that autonomous "stashed" changes.**
The cycle found uncommitted changes in the project folder and set them aside with `git stash`; the
notification gives the stash name so you can recover them.

**What happens to autonomous when I pause or close the project?**
Pausing the project really stops its autonomous work (running tasks keep their claims) and resuming
starts it again by itself. A closed project's autonomous work stays stopped.

**Restarting or updating a worker's CLI — will it break a running task?**
No. Restarts and CLI updates wait for the work in progress to finish; meanwhile the worker shows a
**Restarting** tag and new commands get a "the worker is restarting" message.

**Is there a limit on how many rows the AI can add?**
Yes — new rows per book per month depend on your plan (Free 300, Pro 1 000, Max 5 000). At the cap new
requests wait (managers are notified and Last check says so) but approved tasks are still implemented.

**Can old task branches be cleaned up?**
Yes — **Git › Branch cleanup** lists dead branches to delete (and restore). An ADMIN / PM can turn on
**Daily branch cleanup** in the autonomous settings. See [Git operations](./git-operations.md).
