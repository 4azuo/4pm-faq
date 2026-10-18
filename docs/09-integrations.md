# Integrations & sync

4PM can connect to external tools and keep work items in sync **both ways**. You connect a provider
to your org/project, 4PM mirrors its data, and changes flow in both directions.

| Provider | Project sync |
| --- | --- |
| **GitHub** (issues) | ✅ — reuse the project's **GitHub App** (give it *Issues: read & write*), or a repository + personal access token. |
| **Jira** | ✅ — sign in with Jira (OAuth) and pick the **exact Jira project**; one 4PM project links to one Jira project. |
| **Backlog**, **Confluence** | Shown as *Coming soon* — not connectable yet. |

Integrations need the **Pro** plan or higher. Connecting, resyncing and disconnecting need the
integration-connect permission (**ADMIN** and the project's **PM** by default); every member can read the
synced data.

## Connect a provider

Connections are **per project**: project › **Settings** › **Sync with external tools**, one tab per provider.

**GitHub**
1. If the project uses a **GitHub App** for git, press **Use GitHub App** — make sure the App has *Issues:
   read & write* on the repo.
2. Otherwise type the **Repository** (`owner/repo`) and an **Access token** (a personal access token with repo
   access; stored encrypted, never shown again) and press **Connect**.

**Jira**
1. Press **Connect** — you're sent to Atlassian to authorize 4PM.
2. Back in 4PM, pick the **Jira site**, then the **Jira project**, and press **Link project**.

After connecting, 4PM registers a webhook and **backfills** the existing issues and milestones; the
connection becomes **active** when the import finishes. **Resync** imports everything again; **Disconnect**
stops the sync (nothing is deleted on the provider).

## View synced data

Once connected, the project's **Community** tab shows the imported data — see below. Updates arrive in real
time as they happen on either side. ADMIN / PM (and workers) can create, edit and delete work items there;
deleting one closes or deletes the issue on the provider.

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

## Where synced data shows up

- The project's **Community** tab: **Issues**, **Tasks**, **Milestones** (and Pages) with a source badge.
- The project's Content charts: a **delivery timeline / roadmap** of milestones, **burndown, burnup and
  cumulative-flow** charts, and a **Gantt** chart of items with start/due dates (with dependency arrows
  for blocking Jira issues).

## Reliability

- Sync runs through background workers, so large imports and bursts of changes don't block you.
- If a webhook is ever missed, a periodic reconcile compares both sides and heals the difference —
  webhooks are the fast path, reconcile is the correcting path.

## Linking requests to issues

Once a project has an active connection, its synced issues can drive the task books:

- **Link an issue** (User Todo row) — pick a synced issue (search by key or title). The **Issue** column shows a
  chip with the provider, key and status. One issue links to one request per project. The link is stored in the
  repo as `jira:KEY-12`, `backlog:KEY-3` or `github:owner/repo#12`, readable without 4PM.
- **From issue** (User Todo add menu) — create **Pending** requests from one or more issues: title and description,
  due date, and the labels that match a project tag code (other labels are dropped, with a notice).
- **Discussions** can list **Linked issues** (several; link only, no sync).

What syncs, per linked request:

| Field | 4PM → issue | Issue → 4PM |
| --- | --- | --- |
| Title / description | ✔ | ✔ — held for review on an approved request |
| Due date | ✔ | ✔ |
| Tags ↔ labels (by tag code) | ✔ | ✔ |
| Status | ✔ | ✘ — 4PM resets it |

- **Newest edit wins** per field; both values are recorded in the row's **Sync history**.
- **Status follows 4PM:** pending / approved → open, tasks running → in progress, all tasks done and merged → done,
  trashed → closed. Once the request is approved or taken in, 4PM appends a short note to the issue asking people to
  discuss changes in 4PM. After intake only the status syncs.
- **Approved requests are protected:** an inbound title / description edit waits as an **external change**, shown on
  the row and in **My work › External changes** — apply it (the approval becomes stale) or keep 4PM's text (written
  back to the issue). Due date and tags apply at once.
- **GitHub due date:** a `Due: YYYY-MM-DD` line at the end of the issue body.
- Imported requests count toward the plan's monthly book rows. Backlog links need a Backlog connection, which isn't
  available from Settings yet.

See also: [Tags, due dates & My work](../faq/tags-and-my-work.md).

## Troubleshooting

- **"Connected but no data"** — the backfill may still be running; watch the progress indicator, or press
  **Resync**.
- **"An issue edit didn't reach my request"** — the request is approved: review it in My work › External changes.
- **"I can't find the Integrations page"** — it was retired; connections are in project › Settings › Sync
  with external tools.
- **"The integration service is offline"** — the sync service is unreachable for a moment; try again later.
- **"Couldn't reach Jira"** — reconnect Jira (the authorization may have been revoked or expired).
- **"My change didn't reach the provider"** — check the item isn't stuck **pending**; a provider
  auth or webhook issue can delay egress. Reconnect if the token was revoked.
- **"My change was overwritten"** — that's the **4PM-wins** policy after a simultaneous edit; the
  provider's version is kept in the item's record.

See also: [Integrations FAQ](../faq/integrations.md).
