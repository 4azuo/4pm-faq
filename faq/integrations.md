# Integrations & sync

**Which tools can I connect?**
**GitHub** (issues) and **Jira**, synced **both ways**. **Backlog** and **Confluence** are shown as *Coming
soon* and can't be connected yet. Integrations need the **Pro** plan or higher. See
[docs/09](../docs/09-integrations.md).

**Where do I connect them? I can't find the Integrations page.**
The old Integrations page was retired. Connections are **per project**: project › **Settings** › **Sync with
external tools**, one tab per provider. You need to be an ADMIN or the project's PM (integration-connect
permission).

**How do I link GitHub issues?**
If the project uses a **GitHub App** for git, press **Use GitHub App** (give the App *Issues: read & write*).
Otherwise enter the **Repository** (`owner/repo`) and a personal **access token** with repo access, then
**Connect**. The token is stored encrypted and never shown again.

**How do I link Jira?**
Press **Connect**, authorize 4PM at Atlassian, then pick the **Jira site** and the **exact Jira project**
and press **Link project**. One 4PM project links to one Jira project.

**When will Backlog work?**
It's on the roadmap (shown as *Coming soon*); there is no date yet.

**Where do synced issues show up?**
In the User Todo rows you link them to (see below), and in the project's **Community** tab: **Issues**, **Tasks**, **Milestones** and **Pages**, each with a source
badge — plus the roadmap, burndown/burnup, cumulative-flow and Gantt charts in Content. ADMIN / PM can
create, edit and delete work items there; deleting one closes or deletes the issue on the provider.

**Can I link a User Todo request to an issue?**
Yes. In User Todo, open a row and use **Link an issue**: pick one of the project's synced issues (search by key
or title). The **Issue** column then shows a chip (provider, key, status) that opens the issue. One issue can be
linked to only one request per project. The project needs an active connection (above); linking needs the right
to write the book.

**Can I create requests from issues?**
Yes — **From issue** in User Todo's add menu: pick one or more issues; each becomes a **Pending** request with the
issue's title and description, due date and the labels that match a project tag code (other labels are listed
and not copied). Save the grid to keep them. You're the author, so someone else approves them, as usual.

**What syncs between a linked request and its issue?**
| Field | 4PM → issue | Issue → 4PM |
| --- | --- | --- |
| Title / description | ✔ | ✔ (see approved rows below) |
| Due date | ✔ | ✔ |
| Tags ↔ labels (labels named like a tag code) | ✔ | ✔ |
| Status | ✔ | ✘ — always set by 4PM |

For each field the **newest edit wins**; the overwritten value is kept in the row's **Sync history**. On GitHub,
which has no due-date field, the date is a `Due: 2026-11-30` line at the end of the issue body — edit or delete
that line to change or clear it.

**How does the issue status follow 4PM?**
Pending or approved → **open**; the AI works on its tasks → **in progress**; all tasks done and merged → **done**;
request moved to trash → **closed**. Moving or closing the issue in Jira / GitHub doesn't change the request — 4PM
sets the status back. Once the request is approved or taken in, 4PM adds a short note at the end of the issue
asking people to discuss changes in 4PM.

**Someone edited the issue of an approved request — why didn't 4PM update?**
Applying it would un-approve the request and stop running work, so the edit **waits for you**: review it from the
row or from **My work › External changes**, then **apply** it (the approval becomes stale, as with any edit) or
**keep 4PM's text** (it's written back to the issue). Due date and tags apply at once — they don't affect the
approval. Once the AI has taken the request in, only the status still syncs.

**The issue was deleted.**
The chip shows it; the request stays. Unlink it from the row if you like.

**Can a discussion link issues?**
Yes — **Linked issues** when you open or edit a discussion (several allowed). Discussions are only linked, not
synced.

**Does Backlog work?**
Links accept Backlog issues, but a Backlog connection can't be set up from Settings yet (*Coming soon*), so only
Jira and GitHub issues can be linked for now.

**I connected but see no data.**
The **backfill** may still be running — watch the progress indicator, or press **Resync**. The connection
becomes **active** when it finishes.

**Does sync go both ways?**
Yes. Edits in 4PM are pushed out to the provider (the item shows **pending** until confirmed), and
provider-side changes come back via webhook.

**Both sides changed the same item — which wins?**
**4PM wins.** 4PM keeps its own value and applies it to the provider, and notifies you of the override (the
provider's version is kept in the item's record for reference).

**My change didn't reach the provider.**
Check the item isn't stuck **pending** — a provider auth or webhook problem can delay egress. Reconnect if
the token was revoked ("Couldn't reach Jira" means the Jira authorization must be renewed).

**What if a webhook is missed?**
A periodic reconcile compares both sides and heals any difference, so missed webhooks self-correct over
time.

**How do I stop syncing?**
**Disconnect** in the provider's tab. Nothing is deleted on the provider; connect again later to resume the
sync.
