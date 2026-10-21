# Projects

**How do I create a project?**
Use the two-step wizard: step 1 is basic info (name, description, and an **idle machine-user**);
step 2 is the details/spec. Then press **Create** and 4PM scaffolds it on the worker. Full flow:
[docs/05](../docs/05-projects.md).

**Can I use an existing repo instead of a new one?**
Yes — use **Add existing**, if the repo already has a 4PM spec (`project.spec.json`) on the branch you
declare. The wizard reads that spec and shows it read-only; you only fill in the Git section. 4PM
clones the repo onto the worker and marks the project **ready** — no scaffold or AI init runs. A repo
without a 4PM spec can't be added; create a new project instead.

**Can a project have several repositories?**
A project is **one** repository. Add other repos as **git submodules** — in the wizard's Git section,
or later in **Git › Configuration**. See [docs/05](../docs/05-projects.md#the-git-section-repository-branch-submodules-authentication).

**Which branch does 4PM commit to?**
The branch you declare is the project's **base branch**: the scaffold is committed and pushed straight
into it (no PR to the default branch). If it doesn't exist, the wizard lets you create it from the
default branch, another branch, or empty.

**Create is blocked because the branch is protected.**
The scaffold push can't land on a protected branch. Unprotect it for the creation, then protect it
again — autonomous mode never pushes to the base branch.

**Create is blocked because the worker has no CLI for the AI provider.**
The project's AI provider (Claude or Codex, chosen in the spec's AI guide section) must be installed
on the worker. Workers install it automatically; otherwise install it from the worker's
[Tools tab](../docs/14-worker-tools.md).

**Creation says "no idle machine-user".**
You need a paired CLI that isn't already serving a project. Pair a worker first
([docs/03](../docs/03-connect-a-worker.md)) or free one up, then retry.

**Do I choose where the project folder goes?**
No. The CLI derives the working folder from the project name and reports the path back — there's
no folder picker.

**What is the "spec"?**
A description of what the project is and what to build. You edit it with AI help — **Suggest**,
**Review** (an overall assessment) and **Compose** (rewrite from the review). See
[docs/05](../docs/05-projects.md#the-spec-and-ai-assist).

**What is the "Output language" field in the spec?**
Spec › **1. Basic** › **Output language** — the language the AI writes this project's **repo content** in:
documents (README, the AI guide, `docs/…`, the evidence guide), code comments and log messages it adds,
commit messages, pull-request titles and bodies, and book rows. Pick one from the list (English, Tiếng Việt,
日本語, 中文, 한국어, Français, Deutsch, Español, Português, ไทย, Bahasa Indonesia) or **Other…** and type a
language name. It is saved with the spec, so the whole team shares it.

- **Empty** (the default) = no rule: the AI follows the language of what it reads, as before.
- Code identifiers, file and folder names, paths, IDs (`TSK-…`), JSON keys and commit types (`feat(…)`) never
  change.
- Product text shown to *your* users still follows the project's own i18n, not this field.
- It isn't retroactive: rows and docs written earlier keep their language. The AI guide gets a line stating
  the rule when it is generated, so a free-typed Console run follows it too.
- The 4PM screens' language is your own UI language (profile menu) — unrelated to this field.

**Review / compose locked my form.**
That's on purpose: while AI review or compose rewrites the spec, the form is locked so your edits
aren't overwritten. It unlocks when the run finishes.

**Will I lose my spec if I switch tabs or log out?**
Switching tabs keeps it (client cache). Press **Save draft** to persist it server-side so it
survives logout and closing the browser; **Load draft** reads it back. You can also
**Export/Import** it as a file.

**What do the project states mean?**
`draft` = created but not built; `ready` = scaffolded/cloned and serving on the worker (you can
run commands, Git and autonomous mode); `paused` = read-only for operations; `closed` = read-only
until reopened.

**Creation failed partway — what now?**
Creation runs as a background job that reports **which step** failed; click **Create** again to
retry. If only the final push or pull request failed, the project is ready and shows a warning with
**Retry push**.

**Can I change the repo, branch or git auth after creation?**
Yes — in the **Git** tab's **Configuration** section (add/remove submodules, switch the branch, set
git authentication). It works even while the worker is offline. You need the git-configuration
permission (ADMIN/PM by default, grantable to a member).
