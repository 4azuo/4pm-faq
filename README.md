# 4pm-faq

The **shared knowledge base** for 4PM's AI support agents — product **docs** + **FAQ**, kept in
git and read directly by the agents to answer "how do I use 4PM" questions.

**Decision:** [ADR-0170](https://github.com/4azuo/4PM/blob/main/11-docs/11-adr/0170-ai-support-agents-shared-repo-no-rag.md)
— support agents clone/pull this repo and answer from it (no RAG index). It is a plain content
repo, **isolated from customer projects**, edited here in git by the platform team.

## Layout

| Path | Holds |
| --- | --- |
| `faq/` | Frequently-asked questions, one topic per markdown file. |
| `docs/` | Product usage docs ("how to use 4PM") the agents cite by heading/path. |

## Conventions

- **Markdown only**, English (matches the 4PM docs language convention).
- One topic per file; a short `#` title at the top; keep answers task-oriented.
- No secrets, no customer data — this repo is the public-facing product knowledge only.
