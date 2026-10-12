# Worker configuration

Each worker CLI has a **config** (`config.json` in its profile) that decides which AI accounts it
uses, how it fails over between them, its time limits, memory and console behaviour. You edit it
**from the web** — no need to log into the machine.

## Where to edit it

- **One worker:** open the machine-user's page › **Settings** › **Worker configs**. The worker must be
  **connected**. You get a **Form** tab and a raw **JSON** tab over the same config.
- **Many workers:** **Machines › Configs** holds named **config templates**. Create one, then **Apply** it
  to selected machine-users — online workers change now, offline ones on their next connect. Every save
  keeps a **version** you can view and restore, and an ADMIN can mark one template as the **default** for
  new machine-users. (Applying overwrites the worker's config; later edits to either don't sync.)

Who can edit: ADMINs, and PMs for the workers of projects they manage. Rented (4PM-hosted) workers are
managed by 4PM. Fields that 4PM manages for the project are preserved when you save.

## AI profiles (accounts)

A **profile** is one AI account the worker can use: a **provider** (Claude or Codex), a **profile
directory** (where that account's login lives, e.g. `.claude`), an optional **model**, extra
**arguments**, and an **enabled** switch.

- **Order = priority.** Drag profiles to reorder: the top one is tried first.
- **Failover:** if an account is signed out, out of credits, rate-limited or over its usage limit, the
  worker moves to the next profile automatically — even across providers when the list mixes Claude and
  Codex.
- **Failover start:** *Remember last working* (default — start from the account that worked last) or
  *Always top priority*.
- **Active AI CLI:** pin runs to one provider's profiles, or "—" to use the whole mixed list.
- **Model:** pick from the models the worker's CLI supports, or leave the default.
- **Each profile needs its own directory** — two profiles on the same directory are the same account,
  so saving is blocked.
- **Disable** a profile to keep it without using it.
- **API key (Claude):** instead of a signed-in login, a Claude profile can use an Anthropic API key —
  stored in 4PM (write-only), or read from **AWS SSM Parameter Store** or **AWS Secrets Manager**.
- **Mounted logins:** when the container mounts AI logins from the host (see
  [Install & run the CLI](./15-install-cli.md)), each is added as a profile automatically and the
  directory box suggests them.

Sign a profile in with `4pm ai-login` on the worker. From the web Console, `/ai-profile` lists the
profiles and `/ai-profile use N` switches the active one.

On a project, the Machine users list shows which **AI accounts** each worker uses.

## General settings

| Setting | Meaning |
| --- | --- |
| **Auto-update on startup** | Update the CLI when it starts (on by default). |
| **AI run time limit (seconds)** | Stop a single AI run after this long (default 300; 0 = no limit). A project can override it in its Settings. Autonomous runs use their own timeout. |
| **Tool install timeout (s)** | Per-attempt limit for installing/updating a worker tool (default 300). |
| **CLI language** | Language of the worker's own messages (blank = follow the machine, then English). |
| **Command-history upload interval** | How often the command history is uploaded (minutes). |
| **Environment variables** | Extra variables passed to the AI CLI. |

## Console settings

| Setting | Meaning |
| --- | --- |
| **Web Console commands** | Tick the `4pm` slash commands the web Console may **not** run. Default blocks `/quit` and `/config`. Someone at the machine keeps every command. |
| **Auto-clear idle transcript** | Clear the TUI transcript after this many idle minutes (a project can override it). |
| **Shared AI memory** + **memory budget** | Keep a short summary of the conversation that survives switching worker, model or account (off by default; costs an extra small AI call per turn). A project can override it. |
| **Continue the AI conversation within (minutes)** / **Largest conversation to continue (tokens)** | A Console prompt continues the previous conversation only if it's recent (default 5 min) and small (default 100 000 tokens); otherwise a fresh one starts from the shared memory. Continuing a long conversation re-sends it on every turn, which costs tokens. |

## Related settings elsewhere

- **Worker tools** (installed CLIs, auto-update per tool): the machine-user's **Tools** tab — see
  [Worker tools](./14-worker-tools.md).
- **Per-project** limits (AI run timeout, idle auto-clear, memory, per-prompt token limit): the project's
  **Settings**.
- **Network** and **MCP** rules for AI runs: per project — see
  [Project content](./25-project-content.md#networks).
- **Pools and routing** (which worker runs which AI job): see
  [Worker pools & AI routing](./24-worker-pools-and-routing.md).

See also: [Recommended setup](./22-recommended-setup.md) ·
[CLI & worker config FAQ](../faq/cli-and-worker-config.md).
