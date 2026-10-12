# Task books, approvals & discussions

The **books** are the tables that feed [autonomous mode](./08-autonomous-mode.md): people post
**requests**, the AI turns them into **tasks** and asks **questions**, and nothing runs until it is
**approved**. You find them in Project › **Content** › **AI content**.

| Book | Row id | What it holds |
| --- | --- | --- |
| **User Todo** | `REQ-000123-001` | Requests from team members and customers. |
| **User Q&A** | `QA-000123-001` | Questions the **AI** asks. You only answer them here. |
| **AI Todo** | `TSK-000123-001` | Tasks the AI will implement (from intake, from people, or from Draft tasks). |
| **AI Done** | — | Read-only history: each finished task with its group, dependencies, PR links and evidence. |

Row ids are `PREFIX-GROUP-NUMBER`. The **group** ties together the tasks, questions, mockups,
sequence diagrams and branches that came from one request. New ids are reserved by 4PM, so two people
adding rows at once never collide.

## Writing rows

- **Add** rows, edit **Request / Task description / Notes** in a rich editor (formatting, emoji,
  attachments, Preview), and set **Priority**, **Group** and **Depends** (pick from existing ids — a
  task can depend on tasks and on questions).
- **Attachments** (up to 5 MB each) are committed to the repo as **evidence** under `.4pm/evidence`, so
  the AI can open them. **Link a project file** inserts a link to a file in the repo.
- **Deleting** an AI Todo task moves it to **Trash**, where you can restore it for a while (24 h by
  default).
- **Save** sends only the rows you changed — edits by other people and by the AI to other rows are kept.
  If someone changed **the same row** meanwhile, a **conflict review** shows their version next to
  yours; choose which to keep, then save again.
- Unsaved edits survive switching to another item or tab (a dot marks unsaved tabs); they're lost on
  reload.

## The AI menu

On User Todo, User Q&A and AI Todo, one **AI** button opens:

- **Generate** — describe the work; the AI reads the project and its spec and drafts rows as cards you
  can edit, put into a group and make depend on other rows. Add the ones you want as **Pending** rows.
- **Edit** — select rows and describe a change; the AI rewrites them for review. **Approved rows are
  never overwritten** — the change becomes a new row that depends on them.
- **Verify book** — checks every row's group and dependencies (and priority on AI Todo) and suggests
  fixes.
- **Verify business** (AI Verify) — select rows and ask a question; a read-only AI writes an answer per
  row into an **AI verify** column. On **AI Done** it can also propose follow-up work (bug fixes, QA,
  improvements) that you tick and add as Pending rows.

After intake, AI Todo and User Q&A rows can show **View design**: the HTML **mockup** (runs isolated,
no access to your session or the network), the **sequence diagram** and the **ER slice** for that
group.

## Approving

- A row starts **Pending**. Approving it is what lets the AI use it: an approved request is analysed,
  an approved task can be implemented, an approved answer is folded into its task.
- **Four-eyes rule:** you can't approve a row you wrote or edited yourself (ADMIN excepted, unless the
  project has an approval policy) — someone else approves your changes.
- **Signed approvals:** an approval counts only for the exact text that was approved. If the row
  changes afterwards, it shows **Changed after approval** (or **Unsigned** if it wasn't approved through
  4PM) and must be approved again.
- The approve dialog warns when you approve only some tasks of a group, or a task whose dependencies
  aren't approved.
- A row linked to an **open discussion** can't be approved until the discussion is resolved.
- If the group has a pending **ER (data-model) change**, its tasks wait until that change is approved.

Who can write and approve (defaults): **AI Todo** — ADMIN, PM, SA/SE; **User Todo / User Q&A** —
ADMIN, PM, SA/SE, BA. Customers can post requests and answer questions.

## Multi-party approval (Approvals tab)

In the project's **Approvals** tab, ADMINs and the PM (and a team lead for their own teams) can require
more than one approver, per **team** and per **book**:

- the **team lead**, **designated approvers** you choose, and/or the **customer**.
- Each row then shows who has approved so far; it's final only when every required party has approved
  the current text.
- **Ask to approve** notifies the people you pick in-app and by email (you can resend once a day).

Without a policy, one eligible approver is enough.

## Teams on the books

Each row can belong to a **team** (by its team code). The grids filter and group by team, and you can
only change rows of **your own teams** (ADMINs and the PM can change all). Intake copies a request's
team onto its tasks and questions. A worker can be limited to serving certain teams (Members › AI
routing).

## Discussions

**User Q&A holds only the AI's questions.** To ask *people* something — a teammate or the customer —
use **Content › Discussions**:

- Start a discussion, reply, mention people, and **resolve** it when settled.
- **Link** a discussion to a request or task: that row can't be approved until its discussions are
  resolved, and intake reads the resolved discussions as context.
- Discussions opened by customers are highlighted. They're also saved in the repository
  (`.4pm/discussions/`).

## Customers in the books

Customer (CLIENT) accounts can **post requests** in User Todo, **answer** the AI's questions, and open
discussions. Their rows carry a **Customer** badge, and you can sort/filter **Customer first**. See
[Customer accounts](./29-customer-accounts.md).

## Tags on AI Todo

A task can carry **tags** that run a linked action when it's approved — for example syncing the project
spec down to the worker's `project.spec.json`. The approval confirmation lists what each tag will do.

## Plan limits

New rows per book per month are capped by plan (Free 300, Pro 1 000, Max 5 000, Enterprise unlimited).
The Usage tab shows your count.

See also: [Autonomous mode](./08-autonomous-mode.md) ·
[Task books & approvals FAQ](../faq/task-books-and-approvals.md).
