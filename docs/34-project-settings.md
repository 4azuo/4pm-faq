# Project settings

A project's **Settings** tab holds its access, AI limits, budgets and lifecycle. It's for ADMINs, the
project's PM and members granted the project-update permission (team leads don't edit it by default).

## Identity & ownership

- **Project id, name and description** are shown read-only — they come from the spec; edit them in
  Content › Spec and they sync here.
- **Project manager (PM):** one PM per project — an org user with the PM role. Saving replaces the
  current PM.
- **Project group:** place the project in a nested group (e.g. Backend › Services) for the projects list.
- **Copy project:** creates a **draft** copy that inherits this project's spec only — no files are
  created until you run the setup wizard. (Also available from the project's row in the list.)

## Project access & security

- **IP allowlist:** which IPs may open this project on the web/API (one IP or CIDR per line; empty = any).
  It must stay inside the org's allowlist.
- **Restrict AI to the project folder:** every AI prompt tells the agent to read, use and modify only
  content inside the project folder on the worker.

## Session & tokens (AI limits)

These override the worker's own settings for this project (0 = inherit the worker's value):

| Setting | Meaning |
| --- | --- |
| **Session switch %** | When the worker's 5-hour Claude session usage reaches this %, it rotates to the next Claude profile. |
| **Per-prompt token limit** | A single prompt estimated above this is rejected (`PROMPT_TOKEN_LIMIT_EXCEEDED`). |
| **AI run time limit (seconds)** | Stop a single AI run after this long. |
| **Auto-clear idle transcript** | Clear the Console transcript after this many idle minutes. |
| **Shared AI memory** (inherit / on / off) + **memory budget** | Keep a short rolling memory of the conversation across worker, model and account switches. |

## Budgets

- **Token budget:** a limit of AI quota tokens per **day** or **month**; **Block** rejects new runs when
  it's exceeded, **Warn only** just records it. The bar shows tokens used against the budget.
- **Command budget:** a maximum number of commands per period.
- **Usage alerts:** notify by email or in-app when the project's AI usage crosses a threshold (% of the
  budget or an absolute amount) — Pro plan and above.

## Retention & storage

**Messenger retention:** auto-delete conversations inactive longer than N days (capped by your plan; 0 =
keep forever).

## Outbound review

Have a reviewer worker vet **every AI input** before it runs — protecting project secrets and scope:

- **Enable outbound review.** Each input must be approved before the AI runs; push and PR-creating Git
  operations go through the same gate. If no reviewer is available, the input is blocked and the PM is
  notified.
- **Rule check:** a static scan for leaked secrets, out-of-scope paths, other repositories, and commands
  reaching another environment. **Secret rules** and **environment rules** are editable regex lists
  (editing replaces the defaults; empty turns that check off). **Allowed repos** lists the repos commits
  may target (empty = derived from the project's git).
- **AI review:** a reviewer worker also asks its AI to judge the input (no secret values are sent).
- **Outbound reviewers:** the project's machine-users (or a worker pool with the *Outbound review* job)
  that do the reviewing, round-robin; busy or out-of-quota ones are skipped.
- **Block image attachments:** reviews scan text, not images — turn this on to forbid pasting images.

Every input adds a review round-trip (and an AI call when AI review is on), so expect slower runs.

## Lifecycle & danger zone

- **Pause / Resume:** while paused, everything stays readable but operations (AI runs, autonomous) are
  blocked.
- **Close / Reopen:** a closed project is read-only.
- **Delete** the project (danger zone): type the project ID to confirm. It detaches the project's teams,
  members and workers and can't be undone from the UI.

ADMINs/PMs can also pause a single **member**, a whole **team**, or a user within a team for this project,
from the Members tab.

See also: [Create & manage projects](./05-projects.md) · [Organization settings](./33-organization-settings.md).
