# Git operations & merge

The **Git** tab (project › Content › **Git**) lets you do Git from the dashboard. The repo, `git`, and
`gh`/`glab` live on the **worker**; the web builds the Git command, dispatches it to the worker, and
shows you the parsed result. With the **GitHub App** or a **GitLab** credential, 4PM can also read
**origin** directly — even with no worker online.

## What you need

- A **ready** project. For worker views and write actions, a connected worker serving it.
- The right permission:
  - **Read** operations (repositories, branches, graph, history, status, diffs) need the project **git**
    permission.
  - **Write** operations (commit, push, pull, checkout, branch, merge, open PR, edit files) need
    **git-write**.
  - **Configuration** needs the **git configuration** permission (ADMIN/PM by default; a PM can grant it
    to one member of the project).

## Repositories (home)

The **Repositories** view lists the main repository and its **submodules**, each as a collapsible card
with its branch and latest change:

- **Combined graph** — origin, every worker's commits not yet on origin, and each worker's uncommitted
  changes in one view, with per-worker toggles and an "only commits not on origin" filter. Open a file's
  diff straight from it.
- **Origin × workers table** — each worker's branch, how far it's ahead/behind origin, branches never
  pushed, uncommitted changes, last fetch. Offline workers keep showing their last state.
- Select a commit to open **Commit / Changes / File tree** tabs, with added/removed line counts per file
  and folder. Changed files open as an **inline diff**, switchable to side-by-side or to the file content.

## A repository's tab

Each repository has a commit-graph workspace:

- a sidebar of **branches, remotes, tags and stashes** (with ahead/behind or "not pushed" badges, detached
  HEAD and remote-only branches shown);
- the **commit list** (author, SHA, date) and commit details;
- **Local changes** — write the commit message in the rich editor and commit;
- **New branch** / **Checkout** dialogs (checkout says which worker has the branch, can check out a
  remote-only branch, and asks before discarding uncommitted changes);
- **Fetch / Fetch all · Pull · Push · Create PR** (with a target-branch choice), and the pull/merge
  request history.

## Configuration

**Git › Configuration** changes the project's git setup after creation:

- add or remove **git submodules**;
- switch the main repository's **branch**;
- set the **git authentication** — see [Git authentication](./23-git-authentication.md).

It reads only 4PM's own records, so it works even while the worker is offline or the clone is failing.
The Spec tab shows the same block read-only.

## Updating the worker's copy

**Update repos** pulls the latest of the configured branch; **Re-clone** deletes the repo folders and
clones fresh (uncommitted changes on the worker are lost — you're asked to confirm). Both stream their
progress, and are blocked while autonomous mode runs on that worker.

### Outbound review on push / PR

If your project has **outbound review** turned on, `push` and PR-creating operations must pass an
approval gate before they leave the worker. If the input isn't approved (or no reviewer is
available), the operation is blocked and the PM is notified.

## Resolving merge conflicts

When a merge hits conflicts, resolve them from the Git tab by **editing the conflicted files directly**
and then committing the resolution.

## Branches created by 4PM

- The **base branch** you declared receives the scaffold at creation.
- Autonomous tasks use `dev/<base>/<group>/<task>` branches and open PRs into the base branch.
- The task books live on `autonomous-books/<base>` — don't protect it. See
  [Autonomous mode](./08-autonomous-mode.md).

## Troubleshooting

- **"Git tab is empty / spinning"** — the project may not be ready, or no worker is serving it. With a
  GitHub App / GitLab credential you still see origin.
- **"Permission denied on commit/push"** — you likely have read (`git`) but not write (`git-write`)
  permission; ask an ADMIN/PM.
- **"Push blocked"** — outbound review is enabled and the input wasn't approved.
- **Auth errors** — check the project's [git authentication](./23-git-authentication.md).

See also: [Git & merge FAQ](../faq/git-operations.md).
