# Automation rules

A **rule** reacts to something that happens in 4PM: **when** an event occurs (**trigger**), **if**
it matches your **conditions**, **then** run one or more **actions** — notify people, call a webhook,
generate a document, run a checklist with AI, pause autonomous mode, and more.

## Where rules live

- **Organization rules** — Home › **Rules** (ADMIN). They apply to every project. Mark a rule
  **Enforced** so projects can't switch it off.
- **Project rules** — the project's **Rules** tab (ADMIN and the project's PM). The tab also lists the org
  rules that apply here, with a per-project on/off toggle (not for enforced rules), and a **Runs** sub-tab.

## Triggers

| Category | Triggers |
| --- | --- |
| Project | Project created / creation failed · paused, closed, reopened · members changed · spec updated |
| Books | A request / question / task got its **final approval** |
| Checklists | A checklist run completed · a run fell **below its minimum** |
| ER | A data-model change was approved / rejected |
| Operations | A command finished · a worker went offline · a project usage alert fired · network access was blocked |
| Documents | A document was generated · generation failed |
| Autonomous | A task started (claimed), delivered a pull request, finished, failed or timed out · a task was split or ran out of attempts · autonomous paused itself · an autonomous alert |
| Git | A pull request was opened, merged or closed |
| Schedule | A cron schedule (in the org's time zone) |

Some triggers come from the worker, so they need an up-to-date CLI. PR merged/closed are tracked for
projects using the **GitHub App** or a **GitLab** credential (not Self-managed).

## Conditions

- **Filters** on the event's fields (equals, in, contains, greater than, matches…).
- A **time window** (e.g. only during working hours).
- A **throttle** (at most N runs per period).

## Actions

| Action | What it does |
| --- | --- |
| **Notify** | In-app and/or email to users, roles, teams, the PM or whoever caused the event. |
| **Webhook** | HTTPS POST to your URL, signed with an HMAC (`X-4PM-Signature`); 10 s timeout, 3 retries. The secret is shown once after saving. |
| **Generate document** | Generate a document of a [doc type](./30-generators-and-doc-types.md) with fixed parameters. |
| **Run checklist with AI** | A read-only AI runs a checklist; the result is saved as a checklist run. |
| **Custom AI instruction** | A read-only AI answers your instruction about the event; the answer is shown in the run log. |
| **Pause autonomous** | Pause autonomous mode on the project's workers. |
| **Activity log** | Write an entry to the project's History. |

Text fields accept `{{event.<field>}}` placeholders. Actions run in order; a failing action marks the run
**partial** and the rest continue (unless set to stop on failure). AI actions use the project's workers,
a run slot and quota. More triggers and actions are listed as **coming soon** in the editor.

Rules can **never** merge a PR, approve a book row or delete a branch — those stay human.

## Chained rules & the Board

- A rule can follow another: trigger **Another rule finished**, pick the source rule and which results start
  it (succeeded, partial, failed). It can use the source rule's AI output and the original event.
- A link that would make a loop, or a chain of more than **5** rules, is refused. A rule that other rules
  follow can't be deleted. Each run shows which rule's run started it.
- Rules › **Board** shows the rules as lanes — each chain from its trigger, then standalone rules — coloured
  by their last run. Click a rule to see it, or **+** to add a follow-up rule.

## The editor, dry run & run log

- The editor walks you through trigger → conditions → actions (triggers and actions are grouped by
  category) and lists exactly what to fix, on which step, when you save.
- **Dry run** shows what the rule *would* do for an event, with no side effects, and which rules would follow.
- The **Runs** log shows each run: queued, running, succeeded, partial, failed or skipped (with the
  reason), per-action results, and **Retry** for failed actions.
- Runs are kept 30 days by default (org setting).

## Permissions & safety

- A rule runs with its **owner's** permissions. If the owner loses a required permission or leaves, the
  rule is **disabled** and its managers are notified.
- A rule's own actions don't trigger other rules (no chains).

## Plan limits

| | Free | Pro | Max | Enterprise |
| --- | --- | --- | --- | --- |
| Rules you can create (org + project, on or off) | — (not available) | 50 | 100 | unlimited |
| Rule runs per day | — | 500 | 5 000 | unlimited |

Over the daily limit, runs are skipped and ADMINs are notified once a day. The counts show on the Rules
tab and in Usage & quota.

See also: [Automation rules FAQ](../faq/automation-rules.md) · [Checklists](./26-checklists.md).
