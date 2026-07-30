# What is 4PM?

**4PM** is an AI-driven project monitoring & operation platform. You hand a project to 4PM,
it runs command-line AI agents (Claude, Codex) on your **worker machines**, and streams their
progress to a **real-time dashboard** so humans can watch every step and stay in control.

The short version: **hand work to AI, watch it happen live, and control quota, permissions and
billing from one screen.**

## What you can do with it

- **Orchestrate AI agents** — spawn `claude` / `codex` and other CLIs (`git`, `gh`, `glab`,
  shell) on a worker and stream their output back to the browser.
- **Watch in real time** — follow progress, console output and notifications live as the AI works.
- **Create & run projects** — scaffold a new repo or attach an existing one, describe it with an
  AI-assisted spec, then let agents build.
- **Do Git from the dashboard** — browse branches, commit, push, open PRs and resolve conflicts
  without leaving the web app.
- **Run autonomously** — let a project work on a schedule (auto-cycle) while you approve tasks.
- **Integrate your tools** — connect GitHub, Jira, Backlog or Confluence and sync work items
  two ways.
- **Control access & cost** — organizations, teams, roles/permissions, quota and billing.

## Core concepts

| Term | What it means |
| --- | --- |
| **Organization (org)** | Your tenant. Everything — users, projects, billing — lives under an org. The first user created is the **root** user. |
| **User** | A person (or a machine) in an org, with **roles** that grant permissions (ADMIN, PM, TL, etc.). |
| **Machine-user** | A special user that represents a paired worker CLI. You attach it to a project so AI can run there. |
| **Worker** | A physical/virtual machine you control. It runs the `4pm` CLI and the actual AI/Git commands. |
| **CLI** | The `4pm` command-line app installed on a worker. One machine can run several CLIs in parallel; each serves one project. |
| **Project** | A unit of work: a repo (or repos) plus a spec, served by a machine-user's CLI on a worker. |
| **Dashboard** | The web app where you monitor and drive everything. |

## How the pieces fit together

```
You (browser)  ──▶  4PM dashboard  ──▶  server  ──▶  your worker (4pm CLI)  ──▶  claude / git / gh …
      ▲                                                      │
      └──────────────  live output streamed back  ───────────┘
```

1. You **pair** a worker's CLI with your account once (a secure hashcode handshake).
2. You **create a project** and attach a machine-user (the paired CLI) to it.
3. From the dashboard you **dispatch commands** — AI prompts, Git operations, shell — which run
   on the worker.
4. Output **streams back live** to the dashboard, where the whole org can watch.

## Where to go next

- New here? Start with [Accounts & login](./02-accounts-and-login.md), then
  [Connect a worker](./03-connect-a-worker.md).
- Ready to build? See [Create & manage projects](./05-projects.md) and
  [Run AI agents](./06-running-ai-agents.md).
