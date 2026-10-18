# Task books, approvals & discussions

**What are the books?**
Tables in the project repo that drive autonomous mode: **User Todo** (requests), **User Q&A** (the
AI's questions), **AI Todo** (tasks) and **AI Done** (read-only history). See
[docs/28](../docs/28-task-books-and-approvals.md).

**Why can't I approve a row I wrote?**
The **four-eyes rule**: someone else must approve what you wrote or edited (an ADMIN can, unless the
project has an approval policy).

**What does "Changed after approval" / "Unsigned" mean?**
Approvals are signed by 4PM for the exact text approved. If the row changed afterwards — or the
approval wasn't made through 4PM — it no longer counts. Approve it again.

**Why can't I approve this row?**
Possible reasons: you wrote/edited it; you lack the approve permission; a linked **discussion** is still
open; it belongs to another **team**; or the project's approval policy needs you to be a team lead,
designated approver or the customer.

**How do I require the customer or a team lead to approve?**
In the project's **Approvals** tab (ADMIN/PM, or a team lead for their team), set which parties must
approve per team and per book. Use **Ask to approve** to notify them.

**Can I add a question in User Q&A?**
No — User Q&A holds only the AI's questions, and you can only answer them. To ask a person, open a
**Discussion** in Content › Discussions and link it to the row.

**My save showed a conflict.**
Someone changed the same row while you were editing. Pick their version or yours for each row, then
save again. Changes to other rows are merged automatically.

**What do the ids like `TSK-000123-001` mean?**
`PREFIX-GROUP-NUMBER`. The group links the tasks, questions, mockups and branches that came from one
request.

**How do I let the AI write the rows for me?**
Use the **AI** menu: **Generate** drafts rows from a description; **Edit** rewrites selected rows (never
overwriting approved ones); **Verify book** checks groups and dependencies.

**Where are my attachments stored?**
In the repo under `.4pm/evidence`, so the AI can read them (up to 5 MB per file). Finished tasks show
their evidence in AI Done.

**I deleted a task or request by mistake.**
Deleted AI Todo tasks and User Todo requests go to **Trash** — open it in the grid and restore the row
(kept for 24 hours by default). If its ID was taken again meanwhile, you're offered to restore it with a
**new ID**; it then needs approval again, and dependencies on rows that no longer exist are dropped.

**Why can't I delete this row?**
Other rows still **depend** on it — the notice names them. Remove it from their **Depends** first.

**Some AI Todo rows are read-only and show who runs them.**
Those tasks are being run by the AI right now (hover to see since when). You can still **unapprove** one:
the run stops when you save, the work stays on the task branch, and it continues after you approve again.

**How do I start a discussion about a row?**
Click the chat icon on a User Todo, User Q&A or AI Todo row to open a new discussion linked to it (the
open count shows on the icon). A linked row can't be approved until its discussions are resolved.

**What is a DOC row and how do I review it?**
With the docs step on, each request first gets a **DOC** row where the AI writes the request's docs.
Open **Review docs**: each doc file of the round as a diff, the files other open requests also change,
and earlier rounds. Give your opinion, then **Proceed** (accept; the row moves to AI Done and its tasks may
start) or **Revise** (another round with your opinion — required for Revise). Resolve linked discussions
before reviewing. See [Autonomous settings](./autonomous-settings.md#docs-step).

**What do the badges in AI Todo mean?**
**Size S / M** is the AI's estimate (hover for why; bigger work is split). The **Runs** column shows
**Mockup / Sequence / Image / Diagram ×N** when a task has evidence to check.

**How do I tag rows or give them a due date? Where do I see everything waiting on me?**
Use the **Tags** and **Due** columns (changing them keeps the approval), and Home › **My work** for your
cross-project list. See [Tags, due dates & My work](./tags-and-my-work.md).

**Can a request come from a Jira / GitHub issue?**
Yes — **From issue** or **Link an issue** in User Todo; the two stay in sync. See
[Integrations](./integrations.md).

**Where do I see a request's whole journey?**
AI content › **Flow** — one lane per request, from request through docs, tasks and questions to done.

**Can I edit AI Done?**
No, it's a read-only history. Use **AI Verify** on it to check delivered work and propose follow-ups.
