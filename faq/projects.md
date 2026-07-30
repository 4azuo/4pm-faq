# Projects

**How do I create a project?**
Use the two-step wizard: step 1 is basic info (name, description, and an **idle machine-user**);
step 2 is the details/spec. Then press **Create** and 4PM scaffolds it on the worker. Full flow:
[docs/05](../docs/05-projects.md).

**Can I use an existing repo instead of a new one?**
Yes — use **Add**. You provide basic info plus the Git repos; 4PM clones them onto the worker and
marks the project **ready** with an empty spec you can fill in later. No scaffold or AI-init runs.

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

**Will I lose my spec if I switch tabs or log out?**
Switching tabs keeps it (client cache). Press **Save draft** to persist it server-side so it
survives logout and closing the browser; **Load draft** reads it back. You can also
**Export/Import** it as a file.

**What do the project states mean?**
`draft` = created but not built; `ready` = scaffolded/cloned and serving on the worker (you can
run commands, Git and autonomous mode).

**Creation failed partway — what now?**
Creation runs as a background job that reports **which step** failed; you can retry from there.

**Can I add more repos to a project later?**
Yes — a project can have a primary repo and sub-repos; manage Git from the project's
[Git tab](../docs/07-git-operations.md).
