# Autonomous mode & Verify

**What is autonomous mode?**
It lets a project **work on its own on a schedule** — a headless auto-cycle runs on the worker,
picks up approved tasks, and does them, while you observe and approve from the dashboard. See
[docs/08](../docs/08-autonomous-mode.md).

**How do I turn it on/off?**
Two levels, both from the **Autonomous** tab:
- **Pause / Resume** — a soft brake (stops picking up new work, stays installed).
- **Install / Uninstall** — a hard switch that adds/removes the scheduled trigger on the worker.
The CLI applies the change for you; there's no manual worker step.

**Does the AI run tasks without my say-so?**
No. Only tasks you **approve** in the **Verify** panel are eligible to run. Approvals record who
approved each task.

**I approved a task but it didn't run.**
Check its **dependencies** — a task waits until every task it depends on is **done**. It also
won't run if the cycle is **paused** or uninstalled. Review the **tick logs** (by date) for what
happened.

**Can the dashboard and the running cycle conflict over approvals?**
No — the approval state is kept in a separate file from the task list the cycle rewrites, so they
never contend.

**What happens to the schedule if I change the worker or delete the project copy?**
There's one scheduled job per project working copy, and the old CLI removes it automatically on
delete/rename/detach/unlink — so you never get an orphaned trigger.

**Can I send the project an instruction?**
Yes — post a request ("user todo"); it records who posted it.
