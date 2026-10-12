# Recommended setup

A checklist of the choices we recommend for a safe, reliable worker and project. Each item links to
the page with the details.

## Choosing how to run the worker

| Situation | Recommendation |
| --- | --- |
| Trying 4PM on your own laptop / dev machine | **Run directly** (`npm i -g @4pm/cli`, Node ≥ 24). Simple, but the agent runs with your user's access — use a machine without sensitive data. |
| A worker for a team or for real projects | **Docker (headless)** with the `:full` image — the container is the sandbox. |
| You need to control exactly when the CLI changes (audits, change windows) | **`:full-locked`** image — it never updates itself; you upgrade by pulling a newer image. |
| Windows | Run inside **WSL2 (Ubuntu)** — natively the AI toolchain doesn't work properly. |
| You don't want to operate a machine | **Rent** a 4PM machine-user — see [Rented machines](./11-rented-machines.md). |

## Container options

Keep the defaults from the `/cli` page's **Customize** dialog, and add limits:

- **Agent user separation: on.** The AI and project commands can't read the worker's credential,
  config or secrets, and the worker can enforce network rules. Turn it off only if you must share a
  host-mounted AI login directly.
- **Read-only root filesystem, no new privileges, drop capabilities: on** (the defaults).
- **Set resource limits** — at least CPU and memory (e.g. `--cpus 2`, `--memory 8g`) and a process
  limit. The Machines page warns about workers without limits.
- **One container (profile) per project.** A worker serves one project at a time; run several profiles
  for several projects.
- Keep state in the **named volume** so re-creating the container is lossless.

## AI accounts

- Add **two or more AI profiles** (e.g. two Claude accounts, or Claude + Codex) so a run fails over
  when one account hits its limit — see [Worker configuration](./21-worker-config.md#ai-profiles-accounts).
- Give every profile **its own directory**.
- Prefer **mounting** your host's AI logins (one folder per account) or signing in with `4pm ai-login`;
  for API billing, use an **Anthropic API key** stored in AWS SSM / Secrets Manager rather than inline.
- Keep the AI run **time limit** on (default 300 s for interactive runs); raise the **autonomous agent run
  timeout** (default 60 min) only for large tasks.

## Git authentication

In order of preference (details: [Git authentication](./23-git-authentication.md)):

1. **GitHub App** (GitHub) — short-lived tokens, revoked after each job; the key never leaves 4PM.
2. **GitLab service account** (GitLab) — a short-lived, repo-limited token per job.
3. **GitLab token** — works, but it's a long-lived token.
4. **Self-managed** (the worker's own `gh`/`glab` login) — the agent gets that account's **full**
   permissions. If you use it, sign in a **dedicated** account with access to only the repos it needs.

## Branches & autonomous mode

- **Protect the base branch** and require pull requests — 4PM delivers every task as a PR and never
  pushes to it.
- **Don't protect `autonomous-books/<base>`** — the workers write the books there.
- Start autonomous with a few approved tasks; set **quiet hours** and **usage caps** so it doesn't use
  up the AI accounts you also work with.
- Use an **approval policy** (Approvals tab) when a customer or team lead must sign off.

See [Autonomous mode](./08-autonomous-mode.md).

## AI run safety (per project)

- **Networks:** start in **Audit**, review the network log for a few days, then switch to **Enforce**
  with an allow list. AI providers, 4PM and your git hosts are always allowed.
- **MCP servers:** approve only the servers you need; re-approve when their definition changes.
- **AI Security** values: keep test secrets in the write-only secret values, never in the repo.
- Keep **outbound review** on for projects where nothing may leave the worker unchecked.

See [Project content](./25-project-content.md).

## Access

- Require **two-factor authentication** for everyone (Organization Settings › Security), or at least
  keep the default (ADMINs).
- Give the **least** permissions needed: grant a single member a project permission instead of a role
  (Permissions tab); invite customers as **CLIENT** accounts, never as members.
- Use **IP allowlists** for the org and sensitive projects.

## Keeping workers current

- Watch the CLI version badges (amber = update available, red = too old to connect).
- Use **Update all CLIs** (Machines › Machine users) — it skips workers in autonomous mode; update those
  after pausing.
- Turn on per-tool **auto-update** for Claude Code / Codex in the Tools tab, with the org's daily
  maintenance window enabled.

See also: [Install & run the CLI](./15-install-cli.md) · [CLI reference](./20-cli-reference.md).
