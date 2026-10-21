# Organization & project settings

Quick answers first, then what **every setting** means. Fuller pages:
[organization settings](../docs/33-organization-settings.md) · [project settings](../docs/34-project-settings.md) ·
[autonomous settings](./autonomous-settings.md).

## Quick answers

**Where are the organization's settings?**
Home › **Settings** (ADMIN). The sections are explained [below](#organization-settings-explained).

**Where are a project's settings?**
The project's **Settings** tab (ADMIN, the PM, or members granted project-update). The autonomous
schedule and limits are in Content › AI content › Autonomous › Settings — see
[Autonomous settings explained](./autonomous-settings.md).

**How do I make everyone use two-factor authentication?**
Settings › Security › **Two-factor authentication** → *Everyone*. Members without a factor set one up at
their next sign-in.

**How do I make sessions last longer or shorter?**
Settings › **Tokens**: web access/refresh token lifetimes and the CLI session/device-key lifetimes.

**When do workers update their CLI automatically?**
Turn on **CLI · daily auto-update** and pick the hour (org time zone); each idle worker updates and
restarts then (after its running work finishes).

**Which time zone are times shown in?**
Your organization's time zone by default (Settings › General). Each person can pick their own in their
profile **Settings**, or quickly from the profile menu under Language. Column headers that need it name
the zone (e.g. "Claimed at (GMT+7)"), and the header clock shows the time in your zone.

**Where is the audit log?**
In the **Organization** tab, on the Enterprise plan — with filters, details and CSV export.

**How do I cap a project's AI spending?**
Settings › **Token budget** (per day or month; *Block* or *Warn only*) and **Command budget**, plus
**usage alerts**. Per worker, use the machine-user's **Usage limits**.

**How do I change a project's name?**
Edit it in Content › **Spec**; Settings shows it read-only and syncs on save.

**Someone sees "Access restricted" with their IP address.**
The deployment, organization, their account or the project is limited to approved IP addresses. They
send the shown IP to an administrator, who adds it to the right allowlist.

**Which language does the AI write the project's docs, comments and commits in?**
The spec's **Output language** (Content › Spec › 1. Basic) — see [Spec settings that steer the AI](#spec-settings-that-steer-the-ai).

**How do I hide or show columns in a table, or change its page size?**
The table's **⚙ Grid settings**: **Columns**, **Rows per page** (or **Auto** to fit the screen), **Pagination**,
**Remember sort** and **Remember filters**. It applies to that table, for you, in this browser; **Reset to
defaults** undoes it.

**Where are a worker's own settings?**
Home › **Machines** › Machine users › the machine user's page: AI accounts and failover order, models, usage
limits, tools, restart. See [CLI & worker config](./cli-and-worker-config.md). A worker's autonomous schedule is
in the project's Autonomous › Settings — see [Autonomous settings](./autonomous-settings.md).

## Your personal settings explained

Where: the profile menu (top right) › **Settings**, or your user page › **Settings**. Only you see and change
these; they follow you on every device.

| Setting | Meaning |
| --- | --- |
| **Language** | The language of the 4PM screens (English, Tiếng Việt, 日本語, 中文). Also in the profile menu. It doesn't change what the AI writes in a project — that's the project's Output language. |
| **Time zone** | *Organization default* (the org's zone) or your own. Every time in the app — tables, the header clock, analytics days, date filters — is shown in it. Quick switch: profile menu, under Language. |
| **Appearance** | Light, Dark or System (follow the computer). |
| **Theme / Style** | The look of the app — Default, Flat or 8-bit. |

Security items (password, two-factor, passkeys, sign-in methods) are in [Account settings](./account-settings.md).

## Organization settings explained

### General

| Setting | Meaning |
| --- | --- |
| **Time zone** | The org's default zone: used to show times to everyone (unless they pick their own), for schedules, rules, analytics days and the CLI update hour. |
| **Rows per page** | Default number of rows in every table (each grid can still change it). |
| **Idle lock** | Lock the screen of any member idle for this many minutes (0 = off). |
| **Worker config versions kept** | How many versions of each worker-config template are kept; older ones are removed on save. |

### Security

| Setting | Meaning |
| --- | --- |
| **Two-factor authentication** | Who must set up a second factor (authenticator app or passkey): off · ADMINs only (default) · everyone. Machine users are exempt; the root account always needs one. |
| **Password expiry** | 0 = off, up to 365 days. After this many days a member must set a new password at next sign-in. Not applied to root, SSO-only or machine accounts. |
| **Org IP allowlist** | The outer boundary: a user IP outside it is denied, whatever their own list says. Empty = no org-level restriction. One IP or CIDR per line. Sign-in checks only the org's and the user's own list. |
| **Allow sub-accounts without email** | ADMINs may create accounts without email. Those accounts get no email verification or notifications and can't reset a forgotten password themselves — only an ADMIN can. Combined with password expiry, an ADMIN will have to reset their passwords. |

Teams have no IP allowlist of their own: access by IP is set for the organization, each user and each project.

### Tokens (session lifetimes)

Empty = default. Shorter is safer; longer means fewer sign-ins.

| Setting | Meaning |
| --- | --- |
| **Web · access token (minutes)** | How long a web sign-in stays valid before it is silently renewed. |
| **Web · refresh token (days)** | How long you stay signed in without activity. |
| **CLI · WebSocket session token (hours)** | Short-lived token that keeps a worker's realtime connection open; renewed automatically. |
| **CLI · device key (days, 0 = never)** | Lifetime of the credential that identifies a paired machine. When it expires, the machine must pair again. |
| **CLI · max reconnect backoff (5–60 s)** | Longest wait between a disconnected worker's reconnect attempts. |

### Other sections

| Section | Meaning |
| --- | --- |
| **CLI · daily auto-update** + **hour (0–23)** | Every day at that hour (org time zone) each idle CLI updates itself, then restarts. Also enables per-tool auto-update in Worker tools. |
| **Command history** | Whether command history files are kept, and for how many days (0 = forever). When off, recent activity is still recorded. |
| **Community** | How long 4rum posts, Messenger messages and attachments are kept (0 = forever, capped by your plan), and the **edit / delete window** in which authors can change their own post or message (0 = unlimited; admins and moderators can always delete). |
| **AI** | The worker pool that runs org AI tasks outside a project (AI checklist authoring, AI Research). That pool can't also be attached to a project. |
| **Network** | Hosts blocked for **every** project's AI runs. Network logs always keep the last 30 days. |
| **Storage** | Storage by content type (including Marketplace packages, images and Knowledge posts), clearing old content, storage alerts and auto clear. |
| **Marketplace hooks** | Whether projects may install hooks from **other** organizations' packages. Off by default — hooks run commands automatically on agent events, so only official, personal and your org's own packages are allowed. |
| **API integrations** | Every API client in the org and who it acts as; revoke or delete any. |

Caps set by 4PM for your plan (max checklists and versions kept, max worker-config templates) are shown
read-only.

## Project settings explained

### Identity & ownership

| Setting | Meaning |
| --- | --- |
| **Project id / name / description** | Read-only here — they come from the spec (Content › Spec) and sync on save. |
| **Project manager (PM)** | One PM per project; saving replaces the current one. The PM manages the project's settings, rules, autonomous and approvals. |
| **Project group** | Places the project in a nested group (e.g. Backend › Services) in the projects grid. |
| **Copy project** | Creates a **draft** copy with this project's spec only; nothing is created until you run the setup wizard. |

### Spec settings that steer the AI

Some project-wide choices live in the **spec** (Content › Spec), because the AI reads them from the repo:

| Setting | Meaning |
| --- | --- |
| **Output language** (1. Basic) | The language the AI writes this project's repo content in: docs, code comments and log messages it adds, commit messages, pull requests and book rows. Pick a listed language or **Other…** and type one. **Empty = no rule** (the AI follows the language of what it reads). Identifiers, paths, IDs and commit types never change; product text still follows the project's i18n; rows written earlier keep their language. |
| **Doc types** (`docs_types`) | Which kinds of docs the project keeps (ADR, API, screens…). When set, autonomous runs a **docs round** before code — see [Autonomous settings](./autonomous-settings.md#docs-step); the template of each type is in AI content › Doc templates. |
| **AI model** | The model the project's AI CLI uses by default (*Default* = the CLI's own). |

### Tags

**Settings › Tags** — the project's own tags (code, name, color, description), managed by the PM, alongside the
organization's tags (read-only here; ADMINs manage them in Home › Tags). See
[Tags, due dates & My work](./tags-and-my-work.md).

### Sync with external tools

Connect the project to **GitHub** issues or **Jira** (Backlog / Confluence coming soon) — ADMIN / PM. See
[Integrations](./integrations.md).

### Access & security

| Setting | Meaning |
| --- | --- |
| **IP allowlist** | IPs allowed to open this project on the web / API (one IP or CIDR per line; empty = any). Must fit inside the org list. It protects only this project — it doesn't block sign-in. |
| **Restrict AI to the project folder** | Every AI prompt tells the agent to read, use and change only what's inside the project folder on the worker. |

### Session & tokens (AI limits)

They override the worker's own values for this project (0 = use the worker's value).

| Setting | Meaning |
| --- | --- |
| **Session switch %** | When the 5-hour Claude session usage reaches this %, the worker rotates to its next Claude profile. |
| **Per-prompt token limit** | A single prompt estimated above this is rejected — protects against pasting huge inputs. |
| **AI run time limit (seconds)** | Stop a single Console AI run after this long. |
| **Auto-clear idle transcript** | Clear the Console transcript after this many idle minutes. |
| **Shared AI memory** (inherit / on / off) + **memory budget** | Keep a short rolling memory of the conversation across worker, model and account switches; the budget caps its size. |

### Budgets & alerts

| Setting | Meaning |
| --- | --- |
| **Token budget** + period (day / month) + on exceed | A limit of AI tokens for the project. **Block** refuses new runs once it's used up; **Warn only** just records it. The bar shows usage against the budget. |
| **Command budget** | Maximum number of commands per period. |
| **Usage alerts** | Email / in-app notice when AI usage crosses a threshold (% of budget or an absolute amount). Pro plan and above. |

### Retention

**Messenger retention** — auto-delete project conversations inactive for longer than N days (capped by your
plan; 0 = keep forever).

### Outbound review

A reviewer worker checks **every AI input** (and pushes / PRs) before it runs — for leaked secrets,
out-of-scope paths, other repositories and commands reaching another environment.

| Setting | Meaning |
| --- | --- |
| **Enable outbound review** | Each input must pass review before the AI runs. If no reviewer is available, the input is blocked and the PM is notified. |
| **Rule check** + **secret / environment rules** + **allowed repos** | Static scan with editable regex lists (editing replaces the defaults; empty turns that check off). Allowed repos = where commits may go (empty = the project's git). |
| **AI review** | The reviewer also asks its AI to judge the input (no secret values are sent). |
| **Outbound reviewers** | The machine users (or a pool with the *Outbound review* job) that review, in turn. |
| **Block image attachments** | Reviews read text, not images — forbid pasting images. |

Expect slower runs: each input adds a review round-trip.

### Autonomous path

**Send every change through autonomous** (on by default). While the project is ready, the Console, AI
generate and Git writes are refused and changes are posted as **requests** instead; file edits still commit
to the base branch. Turn it off to allow direct runs. See
[Autonomous settings](./autonomous-settings.md#the-project-level-switch-send-every-change-through-autonomous).

### Lifecycle

| Action | Meaning |
| --- | --- |
| **Pause / Resume** | Everything stays readable; AI runs and autonomous stop, and start again on resume. |
| **Close / Reopen** | A closed project is read-only and its autonomous work stays stopped. |
| **Delete** | Type the project ID to confirm. Detaches its teams, members and workers; can't be undone from the UI. |
