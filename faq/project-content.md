# Project content

**Where are the project's files, AI guide and task books?**
In the project's **Content** tab: **Project content** (files, graph, RAG, ER, discussions), **Git**, and
**AI content** (AI guide, task books, autonomous, agents, skills, tools, secrets, networks, MCP). See
[docs/25](../docs/25-project-content.md).

**Content says the worker is unavailable / repositories not set up.**
The serving worker is offline, or its clone failed. Start the worker; for a failed clone fix git
authentication in **Git › Configuration** and click **Retry**.

**How do I edit the AI guide (CLAUDE.md / AGENT.md)?**
AI content › **AI Guide**: edit it, or **Generate** it from the spec. Which file is used is chosen in the
spec's AI guide section.

**An AI run can't reach a website or package registry.**
The project's **Networks** mode is probably **Enforce** and the host isn't allowed. Request access from the
network log, or ask a manager to add it to the allowed hosts.

**My MCP server doesn't start in AI runs.**
Only servers approved in AI content › **MCP servers** start. Scan `.mcp.json` and approve it — and
re-approve after its definition changes.

**Where do I put API keys the project needs for tests?**
In the write-only **secret values** (AI content › AI Placeholder). They stay on the worker and are never
committed — use test values only.

**What is the ER tab?**
The project's approved data model: modules and entities in a side list, an entity panel with fields,
relations and linked docs, and pending changes drawn on the diagram. Propose a change, have it approved,
compare versions, or restore an older one. Tasks that depend on a pending ER change wait until it's
approved (or set **Auto-approve ER changes** in the autonomous settings).

**Can the AI draw the ER for me?**
Yes — **AI draft** (Pro plan and higher): the AI reads the schema in your code and drafts the data model,
which opens in the editor for you to review and save. With no model yet, the tab guides you through it.

**What is the System diagram?**
Project content › **Diagram**: how the system's apps, services, stores, queues and external systems
connect, drawn in a built-in **draw.io** editor. Drag shapes from the "4PM components" library (or set a
shape's *kind* with Edit Data, Ctrl+M); links are http, ws, event, db, file or call. It lives in the repo
as draw.io files, with change requests, approval and version history.

**How do I start the system diagram?**
Draw it yourself in the editor, let a worker AI **draft it from the code** (read-only; you review before
saving), or let autonomous intake propose changes when a request adds components or links.

**Do system-diagram changes need approval?**
Not by default — **Auto-approve system-diagram changes** is on, so a saved change is applied at once.
Turn it off (autonomous settings) to have an approver apply each change; the tasks of its group then wait
(*Diagram pending*). A change that conflicts with one applied since must be revised on the current diagram.

**What is the Evidence guide?**
AI content › Evidences › **Guide**: tell the AI how you want mockups, sequence diagrams, data model, system
diagram and a finished task's proof to look (e.g. "dark admin style, Vietnamese labels, screenshots of
every changed screen"). It's written when the project is created; **regenerate** the whole guide or one
section from a description, review the diff and accept to commit it.

**What does the Evidences screen show?**
Each mockup / sequence / diagram with its task status (Done, In progress, Approved, Pending…) and when the
file last changed, grouped by request. Mockups and sequences have a **History**: view an earlier version,
compare it with the current one and **restore** it (saved as a new version).

**What does the Graph tab do?**
It maps your docs and code: filter by kind, status and feature, search features, and switch between a
**graph** and a **tree**. The **structure score** (1–100) flags docs nested too deep, orphans, broken links
and unclassified docs — click a number to filter to them. **AI review** (Pro and higher) proposes concrete
moves to improve the structure.

**How do I use RAG search?**
The **RAG** tab searches the repo's documents by meaning: one result per file (other matches expand).
**Ask AI** (Pro and higher) — describe what you need and the AI lists the documents to read, in order.
**Settings**: index status and **Reindex**, minimum score, max results, model. The worker needs no Python;
install shows a checklist of what's missing.

**What is "Open in Docs & AI"?**
On RAG results, AI doc-finder rows and Graph nodes: it jumps to that file in the Docs & AI browser.

**What is the "AI request" button on file screens?**
Describe a change about the open file. When the project sends changes through autonomous it becomes a
**User Todo** request; otherwise the AI edits the project on its worker right away (follow it in the
Console).

**My file save went to the base branch?**
Yes — saving, uploading, moving or deleting in Files, Reports, Tests, Subagents, Skills and CLAUDE.md
**commits straight to the base branch** so every worker gets it. You're warned if someone changed the file
since you opened it.

**What is the "origin/main @ a1b2c3d" label?**
Where Docs & AI, Reports and Tests read their files from — the remote branch and commit. A warning shows
when the project has no remote and the worker's local checkout is shown instead.

**Can I make the Content side menu smaller?**
Yes — collapse it to icons (hover to peek). The choice is remembered.

**How do I update my project to the latest template?**
**Project Template** › **Analyze impact**, then **Update** — it opens a pull request for you to review
and merge (ADMIN/PM).

**My unsaved edits disappeared.**
Edits are kept while you switch Content items or tabs, but not across a page reload or logout. Save
before leaving the page.
