# Worker pools & AI routing

When a project has more than one worker, **AI routing** decides which worker runs which kind of AI
work, in what order, and where it goes when a worker is busy or out of AI budget. **Worker pools** let
you group machines and give them a duty.

## Worker pools (Machines › Pools)

A **pool** is a named group of your machine-users (ADMIN only):

- Create, rename and delete pools; add or remove machine-users (a machine-user belongs to at most one
  pool). Order the members — the first is tried first.
- Set the pool's **default jobs**: which AI jobs it serves and their priority (drag to reorder, toggle to
  enable). These seed a project's routing when you attach the pool.
- **Update** pushes the latest CLI to the pool's online members (rented workers excluded).
- The **Usage** chart shows tokens or commands over time, per pool or per machine-user.

Worker pools need the Pro plan or higher.

## AI jobs

Every AI feature in a project is a **job**: Spec suggest · Spec review · Spec compose · Document
generators · Console agent · Git merge · Graph suggest · Agents/skills generate · Analyze impact ·
Template update · Autonomous mode · Memo to post compose · Outbound review. You never pick a job — each
feature knows which one it is.

## Project AI routing (Members tab)

In the project's **Members › AI routing** (ADMIN/PM):

1. **Attach** pools and/or lone machines. Attaching a pool adds its members to the project.
2. For each entry, set **per job** whether it serves the job and its **priority** (overriding the pool's
   defaults for this project).
3. Optionally choose the **Teams served** — the worker then takes only those teams' autonomous requests
   and tasks (empty = all teams).
4. **Save routing**. Unsaved changes stay highlighted until you save.

How a worker is picked for a job: **pools before lone machines**, then **higher priority**, then the
entry's order; within an entry, the first **idle** worker. A worker is skipped when it's busy, offline,
out of quota, or all its AI accounts are over their limits — the job moves to the next candidate. Only
when every candidate is spent do you get "all workers busy". With no routing entries, any idle worker of
the project is used.

A machine attached to the project is set up automatically: it clones the repo and restores its tools.
If it can't, it shows **Not provisioned** with a notification and a **Retry**.

Other actions on routing entries: **Update** (push the latest CLI), **Update repos** (pull the latest of
the branch) and **Re-clone repos** (fresh clone — discards uncommitted changes on that worker). These are
blocked while the worker runs autonomous mode.

## Default machine-user

The project header has a **default machine-user** picker: the worker your Console and checks use,
remembered per person.

## Run slots & queue

Your plan sets how many AI runs can run **at the same time across the organization** (Free 2, Pro 10,
Max 30). Extra runs wait in a **queue** and start automatically; the Console and progress windows show
your position ("N ahead"). You can stop a queued or running run.

## The org AI pool (Settings › AI)

Some AI work isn't tied to a project — AI checklist authoring, AI Research, and similar. In
**Organization Settings › AI**, pick the **worker pool** that runs these org-level tasks. That pool can't
also be attached to a project.

## Rented machines in pools

A rented machine can be in your pools and routing only while you rent it; when the rental ends it leaves
them automatically.

See also: [Machine-users & workers](./04-machine-users-and-workers.md) ·
[Worker configuration](./21-worker-config.md) · [Worker pools FAQ](../faq/worker-pools-and-routing.md).
