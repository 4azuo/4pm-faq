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

## Reading and working the rows

**Why does each row show only one line?**
The books show **compact rows**: ID, a short **title** with its tag / due / depends chips, group and status.
**Expand** a row (the arrow by its number) to read and edit everything else. The title (up to 80 characters)
is filled in by AI generate, AI edit, the autonomous intake and *From issue*; you can edit it in the row's
details.

**How do I choose which columns a book shows?**
Open the grid's **⚙ Grid settings** › **Columns**. Team, tags, due date, depends and approvers are hidden by
default on the book grids. The same popover sets rows per page and whether sort / filters are remembered — per
grid, in your browser.

**What is the bar at the top of an expanded row?**
The row's **actions as labeled buttons** — approve, discussions, memos, view design, review docs, delete — so
you don't need to go back to the **⋯** menu.

**What do the red and blue marks on the AI content rail mean?**
**Red** always means *waiting on you*: the red count on User Todo, User Q&A and AI Todo is the number of items
for you to approve or answer, and a red dot on **View design** / **Review docs** means an ER or diagram change
or a docs round waits for your review. **Blue** means *changed since you last opened it*. View design links
straight to the waiting change in ER / Diagram › Changes, where you approve it.

**What is the ⚑ N badge by an ID?**
It marks the **root** of a chain: the row that N other rows wait for. Hover it to see which rows wait. Resolve
that row first — the rest follow.

**What is the red "Waiting for" line under a title?**
The requests, questions or tasks that row still waits on (its dependencies, or another request's tasks). It
clears by itself when they're done; the grids re-read the books every 30 seconds while a row is waiting.

**How do I approve or delete many rows at once?**
Tick the rows: the footer shows how many are selected, with **Clear**, **Approve (n)** and **Delete (n)**.
Then **Save** — that signs the approvals, or moves the deleted rows to Trash.

**What's in the row's ⋯ menu?**
Its **discussions** (open one, or start a new one), **My memos** / **New memo** (your private notes on the
row) and the row's other actions. **Approve** stays a separate button.

**Requests stay in User Todo after the AI took them in — why?**
On purpose: a taken-in request is marked **Taken in**, then **Done** when all its tasks are finished, so you
can follow it. It leaves the live book only when it's archived. See [Flow & Archive](./flow-and-archive.md).

**AI Todo shows finished tasks as "Done" rows.**
Those are read-only. The **Status** filter hides Done rows by default — pick **All** or **Done** to see them.

**How do I find tasks that have a mockup, an ER change or a docs round?**
Use the **Runs** filter in AI Todo: by size, or by the evidence a task has (mockup, sequence, ER change,
diagram change, images, DOC round). A DOC row shows **Docs ×N** in Runs, and **View design** has a **Docs**
tab to read its doc files.

**A mockup has several tabs in the viewer.**
One per **state** or server response of the screen (empty, loading, error…), also in full screen.

**What does each book say under its title?**
A one-line reminder of what the book is for — User Todo (your requests), User Q&A (the AI's questions), AI
Todo (tasks to implement), AI Done (what was delivered).

## Delivery in AI Done

**What does the Delivery state mean?**
How the task reached the base branch: **PR open**, **merged**, **closed** (without merge) or **merged
directly** (when the project merges without a pull request). It's refreshed on every autonomous tick.

**What's in an expanded AI Done row?**
**Notes** as labeled lines: the **branch** (with a copy button), the **pull request** link with its state
(Open / Merged / Closed / Merged directly, plus *Conflicts* while it has any), one line per **submodule** pull
request with its own state, and any other remarks. **Show raw** shows the original text.

**How do I see the files a task changed?**
Click **Files (n)** in the expanded row. The left side lists every changed file by repository (root first,
then each submodule) with A / M / D / R badges and a filter; pick one to see its **Content** or its
**Changes** (a diff against the base the task started from). The header says where the files are read from —
the merged commit, the task branch, the pull-request ref or, as a last resort, the base branch (with a warning).
That's why the files stay readable even after **branch cleanup** deleted the task branch.

**An old row shows a shorter file list.**
Rows delivered before the file record existed show the list that was saved then (cut at 20 files); folders
open their contents.

**Can I discuss a finished task?**
Yes — start a discussion from the AI Done row. If it leads to more work, turn the discussion into a
**follow-up request** in User Todo.
