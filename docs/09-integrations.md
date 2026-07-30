# Integrations & sync

4PM can connect to external SaaS tools — **GitHub, Jira, Backlog, Confluence** — and keep work
items in sync **both ways**. You connect a provider to your org/project, 4PM mirrors its data,
and changes flow in both directions.

## Connect a provider

1. Go to **Integrations** and click **Connect** for the provider you want.
2. You're redirected to the provider's consent screen to authorize access.
3. After you approve, 4PM stores the access token **encrypted**, registers a webhook, and starts
   a **backfill** — importing existing data into 4PM.
4. You're returned to the Integrations page; a live progress indicator shows the backfill, and
   the connection becomes **active** when it's done.

## View synced data

Once connected, the **Integrations** board shows the imported **work items** and **milestones**.
Updates arrive in real time as they happen on either side.

## Two-way sync (and who wins)

4PM keeps a normalized mirror of the provider's data and syncs changes both ways:

- **You edit in 4PM (egress).** Creating, editing or deleting a work item in 4PM writes to the
  mirror and queues the change out to the provider. The item shows as **pending** until the
  provider confirms it.
- **The provider changes (ingress).** When something changes on the provider side, its webhook
  notifies 4PM and the change is applied to the mirror.

### Conflict policy: **4PM wins**

If both sides changed the same item at the same time, **4PM's value is kept**. 4PM applies its
own version to the provider and notifies you of the override (the provider's version is retained
in the record for reference). This keeps your dashboard authoritative.

## Reliability

- Sync runs through background workers, so large imports and bursts of changes don't block you.
- If a webhook is ever missed, a periodic reconcile compares both sides and heals the difference —
  webhooks are the fast path, reconcile is the correcting path.

## Troubleshooting

- **"Connected but no data"** — the backfill may still be running; watch the progress indicator.
- **"My change didn't reach the provider"** — check the item isn't stuck **pending**; a provider
  auth or webhook issue can delay egress. Reconnect if the token was revoked.
- **"My change was overwritten"** — that's the **4PM-wins** policy after a simultaneous edit; the
  provider's version is kept in the item's record.

See also: [Integrations FAQ](../faq/integrations.md).
