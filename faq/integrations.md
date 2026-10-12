# Integrations & sync

**Which tools can I connect?**
**GitHub** and **Jira** project sync (Backlog and Confluence project sync are marked *coming soon*).
4PM syncs work items **both ways**. Integrations need the **Pro** plan or higher. See
[docs/09](../docs/09-integrations.md).

**How do I link Jira?**
Sign in with Jira and pick the **exact Jira project** to link — one 4PM project to one Jira project.

**Do I need a separate GitHub connection for issues?**
Not if the project uses a **GitHub App** for git — issue sync can reuse it (give the App *Issues:
read & write*).

**How do I connect a provider?**
Go to **Integrations** → **Connect**, authorize on the provider's consent screen, and 4PM stores
the token encrypted, registers a webhook, and backfills your existing data.

**I connected but see no data.**
The **backfill** may still be running — watch the progress indicator. The connection becomes
**active** when it finishes.

**Does sync go both ways?**
Yes. Edits in 4PM are pushed out to the provider (the item shows **pending** until confirmed), and
provider-side changes come back via webhook.

**Both sides changed the same item — which wins?**
**4PM wins.** 4PM keeps its own value and applies it to the provider, and notifies you of the
override (the provider's version is kept in the item's record for reference).

**My change didn't reach the provider.**
Check the item isn't stuck **pending** — a provider auth or webhook problem can delay egress.
Reconnect if the token was revoked.

**What if a webhook is missed?**
A periodic reconcile compares both sides and heals any difference, so missed webhooks self-correct
over time.
