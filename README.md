# 4pm-faq

The **shared knowledge base** for 4PM's AI support agents — product **docs** + **FAQ**, kept in
git and read directly by the agents to answer "how do I use 4PM" questions.

**Decision:** [ADR-0170](https://github.com/4azuo/4PM/blob/main/11-docs/11-adr/0170-ai-support-agents-shared-repo-no-rag.md)
— support agents clone/pull this repo and answer from it (no RAG index). It is a plain content
repo, **isolated from customer projects**, edited here in git by the platform team.

## Layout

| Path | Holds |
| --- | --- |
| `docs/` | Product usage docs ("how to use 4PM") the agents cite by heading/path. Start at [`docs/README.md`](./docs/README.md). |
| `faq/` | Frequently-asked questions, one topic per markdown file. Start at [`faq/README.md`](./faq/README.md). |

## Contents

**Docs** (task-oriented walkthroughs): [overview](./docs/01-overview.md) ·
[accounts & login](./docs/02-accounts-and-login.md) ·
[connect a worker](./docs/03-connect-a-worker.md) ·
[machine-users & workers](./docs/04-machine-users-and-workers.md) ·
[projects](./docs/05-projects.md) · [running AI agents](./docs/06-running-ai-agents.md) ·
[git operations](./docs/07-git-operations.md) · [autonomous mode](./docs/08-autonomous-mode.md) ·
[integrations](./docs/09-integrations.md) · [billing & plans](./docs/10-billing-and-plans.md) ·
[rented machines](./docs/11-rented-machines.md) · [getting help](./docs/12-getting-help.md).

**FAQ** (quick Q&A): [getting-started](./faq/getting-started.md) ·
[account & login](./faq/account-and-login.md) · [workers & pairing](./faq/workers-and-pairing.md) ·
[projects](./faq/projects.md) · [AI commands](./faq/ai-commands.md) ·
[git operations](./faq/git-operations.md) · [autonomous mode](./faq/autonomous-mode.md) ·
[integrations](./faq/integrations.md) · [billing](./faq/billing.md) ·
[rented machines](./faq/rented-machines.md) · [troubleshooting](./faq/troubleshooting.md).

## Conventions

- **Markdown only**, English (matches the 4PM docs language convention).
- One topic per file; a short `#` title at the top; keep answers task-oriented.
- **User-facing only:** write for end users of 4PM. Do **not** leak internal implementation
  detail (ADR numbers, architecture topics, API IDs, admin-only surfaces) into these files.
- **FAQ ⇒ short Q&A** that summarizes and links to the matching `docs/` page; **docs ⇒ the fuller
  walkthrough**. Keep the two in sync when the product changes.
- No secrets, no customer data — this repo is the public-facing product knowledge only.
