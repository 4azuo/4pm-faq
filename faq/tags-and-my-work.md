# Tags, due dates & My work

## Tags

**What are tags for?**
Labels such as `billing`, `urgent` or `customer-x` that you put on requests, questions, tasks and discussions to
group work by theme, then sort and filter by them (in the books and in My work). Tags also sync with the labels
of a linked Jira / Backlog / GitHub issue.

**Who manages tags, and where?**
- **Organization tags** — Home › **Tags**, ADMIN only. Every project offers them.
- **Project tags** — the project's **Settings › Tags**, managed by the PM. The org tags are listed there
  read-only.

**What does a tag consist of?**
A **code**, a **name**, a **color** (from a fixed palette that reads well in light and dark mode) and an
optional **description**. The code is lowercase letters, digits and `-`, up to 32 characters.

**Why can't I change a tag's code?**
The code is what's written in the books in your repo, so it's fixed once created. Change the **name** instead —
the chips update everywhere.

**"That code is taken."**
A project tag can't reuse the code of an organization tag (or of another tag in the same scope). Pick another
code.

**What happens when I delete a tag?**
Rows that already use it keep the code and show it as a **grey** chip. Nothing in the repo is rewritten.

**How do I tag a row?**
In User Todo, User Q&A, AI Todo (and the read-only AI Done) use the **Tags** column: pick tags from the list.
For a discussion, set them when you open it or with **Edit**.

**Does tagging a row lose its approval?**
No. Tags and due dates are not part of the approved text, so changing them keeps the approval.

**What happened to the "Tag" column in AI Todo?**
It's now called **Actions** — the actions that run when a task is approved (e.g. syncing the spec). Your own
labels go in the new **Tags** column.

## Due dates

**How do I set a due date?**
Use the **Due** column of User Todo, User Q&A, AI Todo or AI Done, or the due field of a discussion. You can sort
and filter by it.

**What do the colors mean?**
**Red** = overdue, **yellow** = due within 3 days.

**Does the AI keep my tags and due dates?**
Yes. When a request is taken in, its tags and due date are carried to the tasks it creates.

## My work

**What is My work?**
Home › **My work**: one list of everything waiting on **you** across all your projects. Items are grouped:

| Group | What's in it |
| --- | --- |
| **In progress** | Your approved requests whose tasks aren't finished yet |
| **To check** | Docs rounds you may review, and finished tasks of your requests (PR open or not checked yet) |
| **To approve** | Rows and approval requests waiting for your approval |
| **To answer** | The AI's questions you can answer |
| **Discussions** | Open discussions that address or mention you |
| **External changes** | Edits made in a linked Jira / Backlog / GitHub issue that wait for your review |

**How do I filter it?**
Pick groups (several at once), tags, a From–To date range, a project, a kind (request, question, task, docs
review, done, discussion, approval request), search ID / title / content, or **Overdue only**. Sort by due,
created, title, project or state.

**What is the timeline?**
Each item drawn from its creation to its due date, zoomable by **week / month / quarter**, with a *Today* line.

**How do I clear a finished task from my list?**
Use **Mark checked** on it. It's a personal mark — it only hides the item for you. **Open the pull request**
takes you to its PR.

**Can I take notes on an item?**
Yes — **Memos** on any row: add personal memos (with images and files). They also appear in your **Memo** tab with
a link back to the item.

**A project says "Not indexed yet".**
My work reads a summary of the books that the project's worker sends. Until a worker serving that project has
come online with an up-to-date CLI, its items don't show. Start the worker (and update its CLI).

See also: [Task books & approvals](./task-books-and-approvals.md) · [Integrations](./integrations.md).
