# Troubleshooting

Quick answers to common "why isn't this working" questions. Follow the links for detail.

**I can't log in.**
- Verify your **email** first (login is blocked until verified).
- Use the right **login mode**: empty *Organization Identifier* for root; the org UUID for org
  users.
- Root users must enter the emailed **6-digit MFA code**.
- Locked out? Too many failed attempts — wait or ask an ADMIN.
See [account-and-login](./account-and-login.md).

**My worker won't pair or connect.**
- Hashcodes expire fast — restart pairing and enter them promptly.
- Check the worker's network/firewall; ensure the CLI is up to date (auto-updates on startup).
- If an old CLI logged out, the same machine-user was paired elsewhere (1:1 rule).
See [workers-and-pairing](./workers-and-pairing.md).

**I can't create a project.**
- "No idle machine-user" ⇒ pair a worker or free one up first.
- Creation is a background job that reports which **step** failed — retry from there.
See [projects](./projects.md).

**My AI command failed.**
- `PROMPT_TOKEN_LIMIT_EXCEEDED` ⇒ prompt too big; shorten it or raise the limit.
- Quota error ⇒ upgrade the plan or buy a scale-pack add-on.
- "Waiting for review"/blocked ⇒ outbound review is on; get the input approved.
- Stuck ⇒ check the machine-user isn't **offline** or **busy**.
See [ai-commands](./ai-commands.md).

**Git won't let me commit/push.**
- Read needs the **git** permission; write needs **git-write** — ask an ADMIN/PM.
- Push blocked ⇒ outbound review; get it approved.
- `gh`/`glab` auth errors ⇒ log those tools in on the worker.
See [git-operations](./git-operations.md).

**An action is "permission denied".**
Your role is missing that **permission**. Ask an ADMIN or PM to grant it.

**Integration isn't syncing.**
- No data yet ⇒ backfill still running.
- Change stuck **pending** ⇒ provider auth/webhook issue; reconnect if the token was revoked.
- Your edit was overwritten ⇒ the **4PM-wins** policy after a simultaneous change.
See [integrations](./integrations.md).

**Billing / access after a failed payment.**
You keep quota during a **grace period** (~a week) before any downgrade to Free. Upgrade or fix
the payment method in /billing. See [billing](./billing.md).

**Still stuck?**
Use the in-app **Help** chat, or escalate to human email support. See
[docs/12](../docs/12-getting-help.md).
