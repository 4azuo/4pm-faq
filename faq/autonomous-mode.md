# Autonomous mode

**What is autonomous mode?**
It lets a project **work on its own on a schedule**: the worker turns approved requests into tasks,
implements approved tasks on their own branches and opens a **pull request** for each — while you
watch and approve from the dashboard. See [docs/08](../docs/08-autonomous-mode.md).

**How do I turn it on/off?**
Project › Content › AI content › **Autonomous** › Overview has a single **Start / Pause** switch.
There's nothing to install on the worker — no cron. Set the schedule in **Settings**.

**Does the AI run tasks without my say-so?**
No. Requests, questions and tasks all need **approval** in the books (User Todo, User Q&A, AI Todo)
before the AI acts on them. Tasks the AI writes start **Pending**. See
[Task books & approvals](./task-books-and-approvals.md).

**Does it merge code into my main branch?**
No. Each task is delivered as a **pull request** into the base branch; you review and merge it. 4PM
never pushes to the base branch, so you can protect it.

**Where is the Verify tab?**
It was removed. You approve rows directly in the books, and **AI Verify** is in each book's **AI** menu.

**What is the `autonomous-books/<base>` branch?**
Where the books and approval records live. It follows your base branch. **Don't protect it** — workers
must push to it; if it's protected, runs stop with a warning.

**I approved a task but it didn't run.** Check that:
- it's still approved (no **Changed after approval** / **Unsigned** badge);
- its **dependencies** are done (two or more dependencies must have their PRs **merged**) and its
  linked questions are answered and approved;
- its group's **ER change** (if any) is approved, and its linked **discussions** are resolved;
- autonomous isn't **paused**, in **quiet hours**, over **max ticks per day** or over the **usage caps**;
- the worker is **online** (an offline worker skips the run) and serves the task's **team**.
Then read the run **Logs**.

**A run stopped part-way through a task.**
Each AI run has a time limit (**Agent run timeout**, 60 minutes by default). The work is pushed to the
task's branch and the task goes back to AI Todo to resume. Raise the timeout in Settings for big tasks.

**Autonomous paused itself.**
It pauses after several failed runs in a row (**Stop on consecutive failures**). Check the Logs, fix
the cause, then press Start. Timeouts that made progress don't count.

**A task was "split into …".**
It failed its maximum attempts (5 by default), so the AI proposed smaller tasks. Approve the new tasks
to continue.

**The AI asked a question in User Q&A.**
The task needs a decision. Answer it (and approve the answer); the task resumes on the next run.

**Which AI model does it use?**
The model of the worker's AI profile. There's no separate autonomous model setting.

**Can several workers work on one project?**
Yes. Each claims a different task, so they never run the same one. You can also limit a worker to
certain **teams** in Members › AI routing.

**Why can't I re-sync the repo or update the CLI on a worker?**
Those actions are blocked while autonomous is running on that worker, so they don't disrupt a task.
Pause autonomous first.

**Is there a limit on how many rows the AI can add?**
Yes — new rows per book per month depend on your plan (Free 100, Pro 500, Max 3 000). At the cap the
AI stops adding rows but keeps implementing approved tasks.
