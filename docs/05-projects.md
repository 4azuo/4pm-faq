# Create & manage projects

A **project** is a repo (or set of repos) plus a **spec**, served by a machine-user's CLI on a
worker. There are two ways to start one: **Create** a brand-new project, or **Add** an existing
repo.

## Prerequisite: an idle machine-user

A project runs on a worker, so you need at least one **idle machine-user** (a paired CLI not yet
serving a project). If you don't have one, pair a worker first — see
[Connect a worker](./03-connect-a-worker.md). If creation reports "no idle machine-user", the
dashboard points you to the machines area to fix it.

## Two-step wizard

### Step 1 — basic info

Enter the project **name**, a **description**, and pick the **idle machine-user** that will serve
it. This creates the project in **draft** state and reserves the machine-user for it.

### Step 2 — details

- **Create (new project):** fill in the **spec** with AI help (see below), then press **Create**.
  4PM scaffolds the project on the worker, sets up Git (via `gh`/`glab`), runs an AI init
  (README, guidance files, a structure skeleton), and marks the project **ready**.
- **Add (existing repo):** you only provide **basic info + the Git repos** (a primary repo and
  optional sub-repos). 4PM clones them onto the worker and marks the project **ready** with an
  empty spec you can fill in later from the **Spec** tab. No scaffold or AI-init runs.

You **don't pick a destination folder** — the CLI derives the working folder from the project
name and reports the path back.

Creation runs as a **background job**; you watch progress live and, if a step fails, you see
which step and can retry.

## The spec (and AI assist)

The spec describes what the project is and what to build. While editing it you get AI help:

- **Suggest** — get AI-generated content for a field.
- **Review** — an overall AI assessment (feasibility, coherence, reasonableness across business,
  security, technical and methodology criteria). Its result is stored with the spec.
- **Compose** — rewrites the whole spec based on the latest review. (Enabled only after a review
  exists; running it clears the old review.)

Each of these runs as an AI command on the project's machine-user, so it uses the same quota and
token limits as any other AI work.

### Saving a spec in progress

- Switching tabs and coming back keeps your in-progress spec (client cache).
- **Save draft** persists it to the server so it survives logout and closing the browser;
  **Load draft** reads it back.
- **Export / Import** moves a spec to a file, so you can carry it between projects or accounts.

## Project states

| State | Meaning |
| --- | --- |
| **draft** | Created (step 1 done) but not yet built. |
| **ready** | Scaffolded/cloned and serving on the worker — you can run commands, Git, autonomous mode. |

## Managing a project

From a project's page you can:

- Open the **Console** to run AI/shell commands and watch output — see
  [Run AI agents](./06-running-ai-agents.md).
- Use the **Git** tab to browse and write to the repo — see [Git operations](./07-git-operations.md).
- Turn on **Autonomous** mode and approve tasks under **Verify** — see
  [Autonomous mode](./08-autonomous-mode.md).
- Edit the **Spec** at any time.
- Connect external tools via **Integrations** — see [Integrations & sync](./09-integrations.md).

See also: [Projects FAQ](../faq/projects.md).
