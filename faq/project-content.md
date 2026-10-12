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
The project's approved data model. Propose a change, have it approved, compare versions, or restore an
older one. Tasks that depend on a pending ER change wait until it's approved.

**How do I update my project to the latest template?**
**Project Template** › **Analyze impact**, then **Update** — it opens a pull request for you to review
and merge (ADMIN/PM).

**My unsaved edits disappeared.**
Edits are kept while you switch Content items or tabs, but not across a page reload or logout. Save
before leaving the page.
