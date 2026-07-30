# Git operations & merge

The **Git tab** of a ready project lets you do Git from the dashboard. The repo, `git`, and the
authenticated `gh`/`glab` CLIs all live on the **worker**; the web builds the Git command,
dispatches it to the worker, and shows you the parsed result.

## What you need

- A **ready** project with a connected CLI serving its working copy (pick it in the machine
  selector if the project has more than one).
- The right permission:
  - **Read** operations (branches, graph, log, status, diff) need the project **git** permission.
  - **Write** operations (commit, push, pull, checkout, merge, open PR, edit files) need the
    project **git-write** permission.

## Browse (read)

From the Git tab you can view:

- **Branches** and a **branch graph**.
- **Commit history / log**.
- **Working status** and **diffs**.

These run as read commands on the worker and render into the branch graph, history and status
views.

## Write

Write operations run on the worker too:

- **Commit** and **push**.
- **Pull** and **checkout**.
- **Merge** branches.
- **Open a pull request** (via `gh`/`glab`).
- **Edit files** directly (for example, to resolve a conflict).

### Outbound review on push / PR

If your project has **outbound review** turned on, `push` and PR-creating operations must pass an
approval gate before they leave the worker. If the input isn't approved (or no reviewer is
available), the operation is blocked and the PM is notified. This is a safety control so nothing
is pushed outward without a check.

## Resolving merge conflicts

When a merge hits conflicts, you resolve them from the Git tab by **editing the conflicted files
directly** and then committing the resolution. The file edit uses a dedicated write channel to the
worker; the rest of the merge flows through the normal Git path.

## Git identity

Commits are made with the project's configured Git identity on the worker. If commits show the
wrong author, check the worker's Git identity configuration for that project.

## Troubleshooting

- **"Git tab is empty / greyed out"** — the project may not be ready, or no CLI is serving the
  selected working copy. Pick a connected machine in the selector.
- **"Permission denied on commit/push"** — you likely have read (`git`) but not write
  (`git-write`) permission; ask an ADMIN/PM.
- **"Push blocked"** — outbound review is enabled and the input wasn't approved. Get it approved
  or ask the PM.
- **Auth errors from `gh`/`glab`** — the worker's `gh`/`glab` must be logged in to the provider.

See also: [Git & merge FAQ](../faq/git-operations.md).
