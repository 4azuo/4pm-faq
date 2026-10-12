# Create & manage projects

A **project** is **one Git repository** (plus any number of **git submodules**) and a **spec**,
served by a machine-user's CLI on a worker. There are two ways to start one: **Create new** (4PM
scaffolds the repo for you) or **Add existing** (a repo that already has a 4PM spec).

## Prerequisite: an idle machine-user

A project runs on a worker, so you need at least one **idle machine-user** (a paired CLI not yet
serving a project). If you don't have one, pair a worker first — see
[Connect a worker](./03-connect-a-worker.md). If creation reports "no idle machine-user", the
dashboard points you to the machines area to fix it.

The worker also needs the **AI CLI** for the AI provider you pick (Claude or Codex). If it's missing,
Create / Add are blocked with an explanation — workers normally install it automatically (see
[Worker tools](./14-worker-tools.md)).

## Two-step wizard

### Step 1 — basic info

Enter the project **name**, a **description**, and pick the **idle machine-user** that will serve
it. This creates the project in **draft** state and reserves the machine-user for it.

### Step 2 — details

The same wizard is used for both modes:

- **Create new:** fill in the **spec** with AI help (see below), set up the **Git** section, then
  press **Create**. 4PM clones the repo on the worker, attaches the submodules, applies the project
  template and spec, runs an AI init (README, the AI guide file, subagents), then **commits and pushes
  straight into the branch you declared**, and marks the project **ready**.
- **Add existing:** only the **Git** section is editable. 4PM reads the repository's
  `project.spec.json` from the declared branch and shows every other section **read-only**. A
  repository without a 4PM spec can't be added. No scaffold or AI init runs; 4PM clones the repo, saves
  the spec and pushes the updated `project.spec.json` to the branch.

You **don't pick a destination folder** — the CLI derives the working folder from the project
name and reports the path back.

Creation runs as a **background job**; you watch progress live and, if a step fails, you see
which step and can retry. If the org is at its limit of parallel AI runs, the AI init waits for a slot
("Waiting for an AI run slot — N ahead…").

## The Git section: repository, branch, submodules, authentication

- **One primary repository** — the project folder *is* that repository. Need more repos? Add them as
  **git submodules**, each at its own folder path (4PM checks duplicate folders/URLs and attaches them
  for you).
- **Branch = the project's base branch.** The branch you enter (for the repo and for each submodule) is
  where the scaffold is committed — there's no pull request to the default branch. The wizard checks
  the branch:
  - **doesn't exist yet** → choose to create it from the default branch, from another branch, or
    **empty** (no history, the scaffold is the first commit);
  - **already exists** → you're asked to confirm before Create;
  - **already has a 4PM scaffold** → the wizard lists which files will be rewritten, with an option
    (on by default) to **reset the 4PM task and progress files** so the new project doesn't inherit old
    tasks;
  - **protected** → Create is blocked, because the scaffold push can't land. Protect it again after
    creation — autonomous mode never pushes to the base branch (see
    [Autonomous mode](./08-autonomous-mode.md)).
- **Git authentication** — how the worker reaches the repo (GitHub App, GitLab service account,
  GitLab token, or the worker's own login). See [Git authentication](./23-git-authentication.md).

After creation you change all of this in the **Git** tab's **Configuration** section — even while the
worker is offline or the clone is failing.

## The spec (and AI assist)

The spec describes what the project is and what to build. It's stored in the repo as
`project.spec.json`, and the AI uses it when drafting tasks. While editing it you get AI help:

- **Suggest** — get AI-generated content for a field or section.
- **Review** — an overall AI assessment (feasibility, coherence, reasonableness across business,
  security, technical and methodology criteria). Its result is saved with the spec.
- **Compose** — revises the spec based on the latest review. (Enabled only after a review exists;
  running it clears the old review.)

Review and compose open a **live progress window** and lock the form while they rewrite it, so your
edits can't be silently overwritten. Each runs as an AI command (same quota and run-slot rules as any
other AI work). If your org has **checklists** bound to these jobs, they gate them — see
[Checklists](./26-checklists.md).

The **Create** button is always available, with a reminder to run AI review & compose first.

### The AI guide section

In the spec's **AI guide** section you choose:

- the **AI provider** (Claude or Codex) and the project's **default model**;
- the project's single **guide file** — `CLAUDE.md` **or** `AGENT.md` — and guidance to put in it
  (with AI suggestions).

### Draft tasks

At the end of the Spec tab, **Draft tasks** analyses the spec with AI into an editable task list, and
**Add to AI Todo** puts those tasks into the AI Todo book for approval (see
[Task books & approvals](./28-task-books-and-approvals.md)).

### Saving a spec in progress

- Switching tabs and coming back keeps your in-progress spec.
- **Save draft** persists it to the server so it survives logout and closing the browser;
  **Load draft** reads it back.
- **Export / Import** moves a spec to a file, so you can carry it between projects or accounts.

## After creation

- If the final **push** or the **pull request** couldn't be made (for example a submodule couldn't be
  attached, or git auth failed), the project still becomes **ready** and shows a warning with the failed
  step and **Retry push**.
- New projects get an `AI_SECURITY.md` written for the project; the AI guide tells the agent to follow
  it.

## Project states

| State | Meaning |
| --- | --- |
| **draft** | Created (step 1 done) but not yet built. |
| **ready** | Scaffolded/cloned and serving on the worker — you can run commands, Git, autonomous mode. |
| **paused** | An ADMIN/PM paused it: you can read everything, but operations (AI runs, autonomous) are blocked. |
| **closed** | Closed: read-only until reopened. |

Pause / Resume and Close / Reopen are in **Settings › Lifecycle** (ADMIN/PM).

## Managing a project

A project's top tabs include **Dashboard · Members · Memo · Community · Content · Console · Spec ·
Generators · Checklists · Rules · Approvals · Usage · Permission · History · Settings** (what you see
depends on your permissions):

- **Content** — the repo files, Git, the AI content (task books, AI guide, agents, skills, network and
  MCP rules…) — see [Project content](./25-project-content.md) and
  [Git operations](./07-git-operations.md).
- **Console** — run AI/shell commands and watch output — see
  [Run AI agents](./06-running-ai-agents.md).
- **Autonomous** (in AI content) — let the AI work on approved tasks — see
  [Autonomous mode](./08-autonomous-mode.md).
- **Members** — people, teams, customers, and the **AI routing** of workers — see
  [Worker pools & AI routing](./24-worker-pools-and-routing.md).
- **Generators**, **Checklists**, **Rules**, **Approvals** — see
  [Generators & doc types](./30-generators-and-doc-types.md), [Checklists](./26-checklists.md),
  [Automation rules](./27-automation-rules.md), [Task books & approvals](./28-task-books-and-approvals.md).
- **Integrations** — connect external tools — see [Integrations & sync](./09-integrations.md).
- **Settings** — access, AI limits, budgets, outbound review, lifecycle — see
  [Project settings](./34-project-settings.md).

Other conveniences: organize projects into nested **project groups** (e.g. Backend › Services) on the
projects list, and **copy a project** from its row in the list.

See also: [Projects FAQ](../faq/projects.md).
