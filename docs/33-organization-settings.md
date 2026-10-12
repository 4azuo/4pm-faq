# Organization settings & administration

Org-wide settings live in Home › **Settings** (ADMIN). The other Home tabs an ADMIN uses to run the
organization are listed at the end.

## Settings sections

| Section | What you set |
| --- | --- |
| **General** | Default **time zone** (used by schedules, rules and the CLI update hour), default **rows per page** in tables, the **idle lock** time for every member (0 = off), how many **worker-config template versions** are kept. |
| **Security** | **Two-factor authentication** policy (off · ADMINs only (default) · everyone), **password expiry** (0–365 days), the **org IP allowlist** (the outer boundary for every user's allowlist), and **allow sub-accounts without email** (such accounts can't use email verification, notifications or self-service password reset). |
| **Tokens** | Session lifetimes: web access token (minutes), web refresh token (days), CLI realtime session token (hours), CLI device key (days, 0 = never expires), CLI max reconnect backoff. Empty = defaults. |
| **CLI · daily auto-update** | Every day at the chosen hour (org time zone), each idle worker updates its CLI and restarts. Also enables per-tool auto-update in Worker tools. |
| **Command history** | Whether command history files are stored, and for how many days. |
| **Community** | Retention of 4rum posts, Messenger messages and attachments (capped by your plan), and the **edit / delete window** for authors (minutes; admins and moderators can always delete). |
| **AI** | The **AI worker pool** that runs org-level AI tasks (AI checklist authoring, AI Research). That pool can't also be attached to a project. |
| **Network** | Hosts blocked for **every** project's AI runs, and how long network logs are kept. See [Project content › Networks](./25-project-content.md#networks). |
| **Storage** | Storage by content type, clearing old content, storage alerts and auto clear. See [Quotas, usage & notifications](./17-quotas-and-notifications.md#storage). |
| **Marketplace hooks** | Whether projects may install hooks from other organizations' packages (off by default). |
| **API integrations** (ADMIN / root) | Every API client of the organization and who it acts as; revoke or delete any. Each person creates their own clients in their profile — see [Public API](./32-public-api.md). |

Some caps (max checklists and versions kept, max worker-config templates) are set for your organization
by 4PM and shown read-only.

## The Organization tab

- Organization info and the **login alias** — a short name members can type as the *Organization
  Identifier* instead of the UUID.
- **Audit log** (Enterprise): every action in the organization, with filters, per-action details and CSV
  export.

## Other admin tabs on Home

| Tab | Use it to |
| --- | --- |
| **Overview** | Counts of users, teams, projects and rented machines, storage, and this month's AI-token usage (visible to every role; the plan name only to ADMINs). |
| **Users** · **Teams** · **Permissions** | Manage people and access — see [Teams, members & permissions](./18-teams-and-permissions.md). |
| **Machines** | Machine-users, workers, pools, links, configs, tools — see [Machine-users & workers](./04-machine-users-and-workers.md). |
| **Docs templates** · **Checklists** | Org libraries — see [Generators](./30-generators-and-doc-types.md) and [Checklists](./26-checklists.md). |
| **Rules** | Org automation rules — see [Automation rules](./27-automation-rules.md). |
| **Announcements** · **Requests** | Messages to people; change-request review — see [Research, announcements & chat](./31-research-announcements-and-chat.md) and [Checklists](./26-checklists.md#change-requests). |
| **Usage** · **Billing** | Plan limits and usage; plan, add-ons and payments — see [Plans, billing & add-ons](./10-billing-and-plans.md). |

## Legal documents & consent

The Terms of Service, Privacy Policy, Acceptable Use Policy, Security Overview, Data Processing Addendum,
Rented Machine Addendum and Add-on Terms are available in your language from the footer. Buying a rental,
extra storage or a scale pack shows the terms that apply; when important terms change you're asked to
review and accept the new version after signing in.

See also: [Accounts & login](./02-accounts-and-login.md) · [Project settings](./34-project-settings.md).
