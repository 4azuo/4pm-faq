# Autonomous mode & Verify

Autonomous mode lets a project **work on its own on a schedule** — a headless "auto-cycle" runs
on the worker, picks up approved tasks, and does them, while you observe and approve from the
dashboard. You drive all of it from the web; there's no manual step on the worker.

## The Autonomous tab

From a project's **Autonomous** panel you can see the current **settings**, **status**, the task
**books**, and pending **approvals**, and control the engine.

### Two on/off levels

- **Pause / Resume** — a *soft brake*. Flips the `paused` flag; the cycle stops picking up new
  work but stays installed.
- **Install / Uninstall** — a *hard switch*. Installs or removes the scheduled job (cron) that
  triggers the cycle on the worker.

Both are done from the web — the CLI applies the change on the worker for you.

## Verify — approving tasks

Autonomous work only runs tasks you've **approved**. In the **Verify** panel you review the AI's
proposed task list and approve or reject each task.

- Approvals are recorded per task, together with **who** approved them (for traceability).
- The approval state is kept in a dedicated file, separate from the task list the cycle rewrites,
  so the dashboard and the running cycle never conflict.
- **Dependencies:** a task waits until every task it depends on is **done**. So even an approved
  task won't start until its prerequisites finish.

You can also post a request/instruction to the project (a "user todo"); that too records who
posted it.

## How a cycle runs (high level)

1. The scheduled trigger fires on the worker.
2. The engine reads your **approvals** and each task's **dependencies**.
3. It runs the next eligible, approved task, and moves finished tasks to the "done" book.
4. Progress and logs are available from the Autonomous tab; you can pull the **tick logs** by
   date.

## Lifecycle & cleanup

There's **one scheduled job per project working copy**. If you delete, rename, detach or unlink a
project's working copy, the old CLI removes its scheduled job automatically — so changing the
CLI, worker or working copy never leaves an orphaned trigger running.

## Tips

- Start with **Pause** off and only a few approved tasks to watch how the cycle behaves.
- Use **dependencies** to sequence work safely instead of approving everything at once.
- Check the **tick logs** if a task didn't run when you expected — it may be waiting on a
  dependency or be un-approved.

See also: [Autonomous mode FAQ](../faq/autonomous-mode.md).
