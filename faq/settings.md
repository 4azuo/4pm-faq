# Organization & project settings

**Where are the organization's settings?**
Home › **Settings** (ADMIN): General (time zone, rows per page, idle lock), Security (2FA policy,
password expiry, org IP allowlist, sub-accounts without email), Tokens (session lifetimes), CLI daily
auto-update, command history, Community, AI pool, Network, Storage and Marketplace hooks. See
[docs/33](../docs/33-organization-settings.md).

**How do I make everyone use two-factor authentication?**
Settings › Security › **Two-factor authentication** → *Everyone*. Members without a factor set one up at
their next sign-in.

**How do I make sessions last longer or shorter?**
Settings › **Tokens**: web access/refresh token lifetimes and the CLI session/device-key lifetimes.

**When do workers update their CLI automatically?**
Turn on **CLI · daily auto-update** and pick the hour (org time zone); each idle worker updates and
restarts then.

**Where is the audit log?**
In the **Organization** tab, on the Enterprise plan — with filters, details and CSV export.

**Where are a project's settings?**
The project's **Settings** tab (ADMIN, the PM, or members granted it): PM, group, IP allowlist,
restrict-to-folder, AI limits, budgets, usage alerts, Messenger retention, outbound review, and
pause/close/delete. See [docs/34](../docs/34-project-settings.md).

**How do I cap a project's AI spending?**
Settings › **Token budget** (per day or month; *Block* or *Warn only*) and **Command budget**, plus
**usage alerts**. Per worker, use the machine-user's **Usage limits**.

**What is outbound review?**
A reviewer worker checks every AI input (and pushes/PRs) for leaked secrets, out-of-scope paths and
other-environment commands — by rules and optionally by AI — before it runs. Turn it on in the project
Settings; it makes runs slower.

**How do I change a project's name?**
Edit it in Content › **Spec**; Settings shows it read-only and syncs on save.
