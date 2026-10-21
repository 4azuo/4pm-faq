# Flow board & Archive

Two views of a project's AI work, both under Project › Content › **AI content**: **Flow** shows where every
request is right now; **Archive** finds finished work later. Everyone with a role on the project can read
them (customers see Flow for their requests too). See [docs/28](../docs/28-task-books-and-approvals.md).

## Flow

**What is the Flow board?**
Each request drawn as one **lane**, left to right: the request (`REQ-…`), its docs round (`DOC-…`), the tasks
(`TSK-…`) and questions (`QA-…`) that came from it, up to **done**. Steps are colored by state (waiting,
approved, running, done…), so you see at a glance which requests are moving and which are stuck.

**What is it for?**
Answering "where is my request?" without opening four books — and spotting what blocks a lane: a question
nobody answered, docs waiting for review, a task waiting on another.

**How do I use it?**
Click a step to open a **quick view** next to it: the full text, team, dependencies and its discussions, with
**Open row** (jumps to the row in its book) and **Open discussions**. A step with discussions shows how many
are open — click the count to open them.

**What are the red steps?**
With **All** selected, deleted requests and tasks are shown in red, with when they were deleted and until when
they can be restored from **Trash**.

**Where do I see why a row waits?**
In the books: a red **Waiting for** line under the row's title names the requests, questions or tasks it still
waits on, and a **⚑ N** badge by an ID marks the row a chain of other rows waits for (hover to see which).
Resolve that one first.

## Archive

**What is the Archive?**
Where finished work goes. A request that has been **done** for longer than **Archive finished requests after
(days)** (Autonomous settings, default 30) moves out of the live books — with its tasks, questions and records —
into `.4pm/archive/` in the repo. Nothing is lost: it stays in git and searchable here.

**How do I search it?**
Filter by **date range**, **book**, **ID**, **text**, **team**, **tag** and **delivery** (PR open, merged, closed or
merged directly). Results are paged; open a result to read the row as it was when it finished.

**Why did a finished request disappear from User Todo?**
It was archived — it's been done longer than the archive age. Find it in **Archive**. Until then, a request
the AI took in stays in User Todo marked **Taken in**, then **Done** when all its tasks are finished.

**Can I change when work is archived?**
Yes — Autonomous › Settings › **Archive finished requests after (days)**. See
[Autonomous settings](./autonomous-settings.md#archive--books-sync).
