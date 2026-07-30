# Git operations & merge

**How do I do Git in 4PM?**
From a ready project's **Git** tab. The repo and `git`/`gh`/`glab` live on the worker; the web
builds the command, runs it there, and shows you the result. See
[docs/07](../docs/07-git-operations.md).

**What can I do from the Git tab?**
- **Read:** branches, branch graph, log/history, status, diffs.
- **Write:** commit, push, pull, checkout, merge, open a PR, and edit files.

**Why is the Git tab empty or greyed out?**
The project may not be **ready**, or no CLI is serving the selected working copy. Pick a connected
machine in the selector.

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

**I get auth errors from `gh`/`glab`.**
The worker's `gh`/`glab` must be logged in to the provider. Authenticate them on the worker.
