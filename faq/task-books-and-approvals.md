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

**I deleted a task by mistake.**
Deleted AI Todo tasks go to **Trash** — open it in the grid and restore the task (kept for 24 hours by
default).

**Can I edit AI Done?**
No, it's a read-only history. Use **AI Verify** on it to check delivered work and propose follow-ups.
