# Project content

A project's **Content** tab is where you browse and edit what's in the repository and how the AI works
on it. It has five groups: **Overview · Project Template · Project content · Git · AI content**.
Unsaved edits in Content items are kept when you switch items or tabs (a dot marks unsaved ones); they're
lost on reload.

If the worker is offline or the repo isn't set up yet, Content shows a notice (with **Retry** when the
clone failed) instead of the files.

## Overview

The project at a glance: its docs structure, AI task progress, and the status of the dependency graph,
RAG and tests.

## Project Template

The scaffold template the project was created from — its **version** and **changelog**. When a newer
template is available, ADMINs/PMs can:

- **Analyze impact** — the AI compares your files with the new template and lists what would change.
- **Update** — the AI applies it on a review branch and opens a **pull request** you review and merge.
  You're notified when that PR is merged or closed.

Both results are saved on the project, so you can come back to them later or refine them with extra
instructions.

## Project content

- **Files** — the repository as a folder tree (you can't go above the project folder): view and edit
  files, new file/folder, rename, delete, drag-and-drop move, **upload** (or paste from the clipboard),
  **download**. Images preview; **Show diff** compares before/after the AI's changes, images included.
- **Graph** — a 3D dependency graph of the docs and code (red = orphan nodes), with a path filter.
- **RAG** — set up retrieval for the project.
- **Reports** and **Tests**.
- **ER** — the project's approved **data model** by module: find an entity and focus on it with its
  neighbours, pan/zoom, or see the whole model in 3D. **Propose a change** (it becomes a change request),
  then approve or reject it, compare versions and restore an older one. Autonomous intake can propose ER
  changes too, and a task waits until its group's ER change is approved.
- **Discussions** — questions between people (members and the customer) — see
  [Task books & approvals](./28-task-books-and-approvals.md#discussions).

## Git

Branches, commits, diffs, pull requests and the project's git configuration — see
[Git operations](./07-git-operations.md).

## AI content

| Item | What it is |
| --- | --- |
| **AI Guide** | The project's single guide file for the AI — `CLAUDE.md` or `AGENT.md` (chosen in the spec). View/edit it, or **Generate** it from the spec (optionally improving the current content). |
| **User Todo · User Q&A · AI Todo · AI Done** | The task books — see [Task books & approvals](./28-task-books-and-approvals.md). |
| **Autonomous** | Start/pause and settings — see [Autonomous mode](./08-autonomous-mode.md). |
| **Evidences** | Every mockup, sequence diagram, ER change and book attachment, grouped by task group and filterable by type. |
| **Agents · Skills** | The project's AI subagents and skills: edit them, generate them with AI, choose a model per subagent. Install more from the [Marketplace](./13-marketplace.md). |
| **Agent tools** | Which tools the AI may use: **Allow** and **Deny** lists — shared for the project (committed), or a local override per machine-user (not committed). |
| **AI Placeholder** & **secret values** | Placeholder keys the project uses, and their values — **write-only** (set or rotate, never shown back), stored on the worker and **never committed**. Use test values only. |
| **AI Security** | The project's security rules for the AI (`AI_SECURITY.md`); the AI guide tells the agent to follow it. Values typed here are never kept when you leave the page. |
| **Networks** | Which hosts AI runs may reach — see below. |
| **MCP servers** | Which MCP servers AI runs may start — see below. |

### Networks

Control the network access of the project's AI runs (the AI CLI, builds, git…):

- **Mode:** **Off** (no filtering, no log) · **Audit** (everything allowed and logged; only blocked hosts
  are stopped — use it to learn what the project needs) · **Enforce** (only allowed hosts; blocked hosts
  always win).
- **Allowed** and **blocked** lists: a host (`pypi.org`), its subdomains (`*.mycorp.com`) or an IP/CIDR,
  optionally a port. AI providers, 4PM and the project's git hosts are **always allowed**.
- **Network log:** what each run connected to, grouped by host. Members can **request** access to a host
  (or ask to block one) from the log; managers approve or reject — nobody approves their own request.
- **Organization Settings › Network:** hosts blocked for every project, and how long the log is kept.
- **Export** the lists for your own AWS DNS Firewall / Network Firewall (for workers on Fargate, which can
  only audit).

Enforcing needs a worker started with the current Docker command (agent user separation on). The
Workers page shows whether each worker **enforces** or only **audits**.

### MCP servers

Only MCP servers you **approve** here start in AI runs — servers declared in the repository's
`.mcp.json` no longer start on their own.

- **Scan** the repository's `.mcp.json` files and approve the servers you need, or add one by hand.
- If a server's definition changes in the repo, it must be **re-approved**.
- **Revoke** a server to stop using it.

## Other project tabs

- **Memo** — notes with status, search and paging, at personal, team or project level; attach images;
  **Compose community post** turns selected notes into a 4rum post with AI.
- **Community** — the project's 4rum news, Messenger, and synced issues/tasks/milestones.
- **Usage** — the project's AI usage and its machine-users.
- **History** — a filterable log of actions on the project, with an analytics view.

See also: [Create & manage projects](./05-projects.md) · [Project content FAQ](../faq/project-content.md).
