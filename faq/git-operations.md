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
From the Git tab, **edit the conflicted files directly** and commit the resolution.

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

**Update repos vs Re-clone?**
**Update repos** pulls the latest; **Re-clone** deletes and clones fresh, discarding uncommitted changes on
that worker. Both are blocked while autonomous mode runs on the worker.
