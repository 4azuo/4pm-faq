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

When a merge hits conflicts, the conflicted files are marked **Conflict** in the Git tab: **Edit** one and
**Save & stage**, or press **Resolve with AI**, then commit the resolution.

## Pull requests

Git › **Pull requests** is a table with state and "only this branch" filters and a button to open each PR on
GitHub / GitLab. A PR the host reports as conflicting is marked **Conflicts**: **Resolve with AI** lets the
AI resolve it on the worker and push the fix (the badge clears once it's pushed; failures are sent to the
managers). For a branch 4PM didn't create you confirm first. Autonomous can do this by itself with *AI
resolves conflicting PRs*.

## Branch cleanup

Git › **Branch cleanup** has two views:

- **Candidates** — branches that look dead: **Merged**, **PR closed**, **Task gone** (4PM task branches whose
  task no longer exists) or **Stale** (no commit for 30 days), with the last commit, PR and the workers that
  hold a local copy. 4PM task branches (except merely stale ones) are pre-selected; others never are.
  **Delete** removes them on the remote and on the workers (a worker copy with unpushed commits is kept).
  Never listed: the base, the books branch, branches with an open PR, a running or pending task's work, and
  checked-out branches.
- **Deleted** — the log of deleted branches with who and when; **Restore** works while the commit still
  exists on the host or a worker.

An ADMIN / PM can turn on **Daily branch cleanup** in the autonomous settings: once a day it deletes 4PM task
branches that are merged, whose PR is closed or whose task is gone, after N days without a commit (14 by
default). Other branches are never deleted automatically.

## Branches created by 4PM

- The **base branch** you declared receives the scaffold at creation.
- Autonomous tasks use `dev/<base>/<group>/<task>` branches and open PRs into the base branch (or merge
  directly when *Merge without a pull request* is on).
- Saving files from the web's file screens commits straight to the base branch.
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
