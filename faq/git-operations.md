# Git operations & merge

**How do I do Git in 4PM?**
From a ready project's **Git** tab. The repo and `git`/`gh`/`glab` live on the worker; the web
builds the command, runs it there, and shows you the result. See
[docs/07](../docs/07-git-operations.md).

**What can I do from the Git tab?**
- **Read:** repositories and submodules, a combined graph of origin + every worker, branches,
  history, status, diffs, commit file trees.
- **Write:** commit, push, pull, fetch, new branch, checkout, merge, open a PR (choosing the target
  branch), and edit files.
- **Configure:** submodules, branch and git authentication (Git › Configuration).

**Why is the Git tab empty or greyed out?**
The project may not be **ready**, or no worker is serving it. Start the worker. Projects using the
GitHub App or a GitLab credential still show origin (branches, PRs, commits) with no worker online.

**I can view Git but can't commit or push.**
Read needs the project **git** permission; write needs **git-write**. Ask an ADMIN/PM to grant
git-write.

**My push was blocked.**
The project has **outbound review** on — `push` and PR operations must be approved before leaving
the worker. Get it approved or ask the PM. If no reviewer is available it stays blocked.

**How do I resolve a merge conflict?**
Conflicted files are marked **Conflict** in the Git tab: **Edit** one and **Save & stage**, or press
**Resolve with AI**, then commit the resolution.

**Where are the pull requests?**
Git › **Pull requests**: a table with state and "only this branch" filters and a button to open each PR on
GitHub / GitLab. If `gh` / `glab` fails you see its error instead of an empty list.

**A pull request shows "Conflicts".**
The host reports that it conflicts with its target branch. Press **Resolve with AI**: the AI resolves the
conflicts on the worker and pushes the fix; the badge clears once it's pushed (a failure is sent to the
managers). On a branch 4PM didn't create you're asked first, since a merge commit is pushed to someone
else's branch. Autonomous can do this by itself — see
[Autonomous settings](./autonomous-settings.md#delivering-tasks).

**How do I clean up old branches?**
Git › **Branch cleanup** › **Candidates** lists branches that look dead — **Merged**, **PR closed**, **Task
gone** or **Stale** (unused for 30 days) — with their last commit, PR and copies on workers. 4PM task branches
(other than merely stale ones) are pre-selected; branches 4PM didn't create never are. Select and **Delete**: they're removed on the remote and the workers. Never listed: the
base, the books branch, branches with an open PR, the work of a running or pending task, and checked-out
branches. A worker copy with unpushed commits is kept.

**I deleted a branch by mistake.**
Git › Branch cleanup › **Deleted** keeps a log of every deletion — press **Restore**. It works while the
commit still exists on the host or on a worker.

**Can branches be cleaned up automatically?**
Yes — an ADMIN / PM can turn on **Daily branch cleanup** in the autonomous settings. It deletes only 4PM task
branches (merged, PR closed or task gone, no commit for 14 days by default); everything is restorable.

**My commits show the wrong author.**
Commits use the project's Git identity **on the worker** — check/adjust that identity for the
project.

**I get auth errors when cloning, pushing or opening a PR.**
Check the project's **git authentication** in Git › Configuration: is the GitHub App installed on that
repo, is the GitLab token valid with the right scopes, or (Self-managed) is the worker's `gh`/`glab`
logged in? See [Git authentication](../docs/23-git-authentication.md).

**Which git authentication should I use?**
GitHub App for GitHub, GitLab service account for GitLab — both give short-lived, per-job tokens. See
[docs/23](../docs/23-git-authentication.md).

**How do I add a submodule or change the branch after creation?**
**Git › Configuration** — it works even while the worker is offline. You need the git configuration
permission.

**What are the `dev/…` and `autonomous-books/…` branches?**
Created by autonomous mode: `dev/<base>/<group>/<task>` holds one task's work (delivered as a PR), and
`autonomous-books/<base>` holds the task books. Don't protect the books branch.

**Does 4PM push to my base branch?**
Only when you ask it to: saving files in the file screens commits to the base branch, and an ADMIN / PM can
turn on **Merge without a pull request** for autonomous tasks. Otherwise all code arrives as pull requests.

**Update repos vs Re-clone?**
**Update repos** pulls the latest; **Re-clone** deletes and clones fresh, discarding uncommitted changes on
that worker. Both are blocked while autonomous mode runs on the worker.
