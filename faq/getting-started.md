# Getting started with 4PM

**What is 4PM?**
An AI-driven project monitoring & operation platform. You hand it a project, it runs command-line
AI agents (Claude / Codex) on your worker machines, and streams their progress to a real-time
dashboard so humans stay in control. See [docs/01-overview](../docs/01-overview.md).

**What's the fastest path from zero to running AI?**
1. **Register** — create your organization with email/password (verify your email) or **Google /
   GitHub SSO** ([docs/02](../docs/02-accounts-and-login.md)).
2. **Pair a worker** — install the `4pm` CLI on a machine and pair it
   ([docs/03](../docs/03-connect-a-worker.md)).
3. **Create a project** — run the two-step wizard and attach your machine-user
   ([docs/05](../docs/05-projects.md)).
4. **Run AI** — open the project Console and dispatch a prompt
   ([docs/06](../docs/06-running-ai-agents.md)).

**Do I need my own machine to run AI?**
Either run your own worker (pair its CLI), or **rent a 4PM-operated machine-user** from the pool
so you don't have to run anything yourself ([docs/11](../docs/11-rented-machines.md)).

**What do I need on the worker?**
The `4pm` CLI (it auto-updates), plus the tools you'll use — typically `git`, `gh`/`glab`, and
`claude` — authenticated as needed.

**Is there a free tier?**
Yes — every organization starts on the **Free** plan. You can upgrade to Pro/Max any time
([docs/10](../docs/10-billing-and-plans.md)).

**How do I get help inside the app?**
Use the **Help** chat bubble for instant AI answers, or escalate to human email support
([docs/12](../docs/12-getting-help.md)).
