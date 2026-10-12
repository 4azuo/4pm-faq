# Troubleshooting

Quick answers to common "why isn't this working" questions. Follow the links for detail.

**I can't log in.**
- Verify your **email** first (login is blocked until verified).
- Use the right **login mode**: empty *Organization Identifier* for root; the org UUID or alias for org
  users.
- Asked for a code or passkey? That's **2FA** — use your authenticator, passkey or a recovery code.
- Locked out? 5 wrong passwords from one network lock it for 15 minutes — wait, or ask an ADMIN.
- Password expired? Set a new one on the screen shown at sign-in.
See [account-and-login](./account-and-login.md).

**My worker won't pair or connect.**
- Pairing codes expire fast — restart pairing and enter them promptly.
- Check the worker's network/firewall.
- CLI version in **red** = too old; the server refuses it. Update it (or pull a newer image).
- If an old CLI logged out, the same machine-user was paired elsewhere (1:1 rule).
- Docker "permission denied" on the volume ⇒ `sudo chown -R 1000:1000 <host-path>`.
See [workers-and-pairing](./workers-and-pairing.md) · [install-cli](./install-cli.md).

**I can't create a project.**
- "No idle machine-user" ⇒ pair a worker or free one up first.
- "No CLI for the AI provider" ⇒ the worker must have Claude/Codex (Worker tools).
- The base branch is **protected** ⇒ unprotect it for the creation.
- Add existing refused ⇒ the repo has no `project.spec.json` on that branch.
- A checklist blocked it ⇒ meet the checklist's minimum or ask a manager.
- Creation reports the failed **step** — click Create again to retry; a failed push shows **Retry push**.
See [projects](./projects.md).

**My AI command failed or is stuck.**
- "Waiting for an AI run slot" ⇒ your org is at its parallel-run limit; it starts automatically.
- Time-limit error ⇒ raise the AI run time limit (project Settings or worker config).
- Session expired / out of credits ⇒ sign the AI account in again (`4pm ai-login`) or add another
  AI profile.
- `PROMPT_TOKEN_LIMIT_EXCEEDED` ⇒ prompt too big; shorten it or raise the limit.
- Quota error ⇒ upgrade the plan or buy a scale pack.
- Blocked for review ⇒ outbound review is on; get the input approved.
- A host can't be reached ⇒ the project's **Networks** rules block it; request access.
- An MCP server isn't available ⇒ approve it in AI content › MCP servers.
See [ai-commands](./ai-commands.md) · [project-content](./project-content.md).

**Autonomous mode isn't doing anything.**
- Is it **started** (not paused, not in quiet hours, under the usage caps and max runs per day)?
- Is the worker **online**, and does it serve the task's team?
- Are the rows **approved** (no "Changed after approval" / "Unsigned" badge), dependencies done,
  questions answered, discussions resolved, ER change approved?
- Is `autonomous-books/<base>` **protected**? Unprotect it.
- Did it **pause itself** after repeated failures? Read the Logs, fix, press Start.
See [autonomous-mode](./autonomous-mode.md) · [task-books-and-approvals](./task-books-and-approvals.md).

**I can't approve a row.**
You wrote/edited it (four-eyes rule), a linked discussion is open, it's another team's row, or the
approval policy needs a team lead / designated approver / the customer. See
[task-books-and-approvals](./task-books-and-approvals.md).

**Git won't let me commit/push, or clone fails.**
- Read needs **git**, write needs **git-write**, configuration needs **git configuration** — ask an
  ADMIN/PM.
- Push blocked ⇒ outbound review; get it approved.
- Auth errors / "Not provisioned" ⇒ fix the project's git authentication in Git › Configuration, then
  Retry.
- "Autonomous is active" ⇒ pause autonomous before re-syncing or updating that worker.
See [git-operations](./git-operations.md).

**An action is "permission denied" or a tab is missing.**
- Your role lacks the **permission** — ask an ADMIN or PM (they can grant it to you on one project).
- Or the feature isn't on your **plan** (teams, chat, pools, integrations, rules, 4rum…).
- Customer accounts only see their projects, read-only.

**A rule didn't fire.**
Check its **Runs** log (skipped by time window / throttle / daily limit?) and the filters. See
[automation-rules](./automation-rules.md).

**Integration isn't syncing.**
- No data yet ⇒ backfill still running.
- Change stuck **pending** ⇒ provider auth/webhook issue; reconnect if the token was revoked.
- Your edit was overwritten ⇒ the **4PM-wins** policy after a simultaneous change.
See [integrations](./integrations.md).

**Storage is full.**
Posting, uploads and new AI runs pause. Free space in Settings › Storage or buy extra storage.

**Billing / access after a failed payment.**
You keep quota during a **grace period** (~a week) before any downgrade to Free. Fix the payment method
in /billing. See [billing](./billing.md).

**Still stuck?**
Use the in-app **Help** chat, or escalate to human email support. See
[docs/12](../docs/12-getting-help.md).
