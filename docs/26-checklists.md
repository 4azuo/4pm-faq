# Checklists

A **checklist** is a reusable list of items to check before an action — for example "the spec names
its user roles", "security requirements are listed", "the request has acceptance criteria". Checklists
are **versioned**, can be bound to **jobs** where they act as a **gate**, and every run is recorded.

## The org library (Home › Checklists)

ADMINs and PMs manage the organization's checklists; everyone can read them.

Each checklist has:

- a **name** and **description**;
- **items** — text, an optional description, and a **required** flag (a required item must pass
  whatever the overall score);
- **jobs** it's bound to (zero or more — a checklist with no job is run by hand or by a rule);
- a **minimum satisfaction %** — below it, the job is blocked. **0 % = advisory**: it never blocks;
  **100 %** = every item must pass.

Saving changed items creates a new **version**; a run always records the exact version it used. Each
checklist's **History** lists its AI authoring runs and versions.

**AI authoring:** describe what to add or change, and the AI edits the current items; review the draft
and save it as a new version. (Runs on the org AI pool — Settings › AI.)

## Change requests

Members who can't edit the library can click **Request a change** on a checklist (or a template file):
write a title and the details of what should change and why. ADMINs/PMs review the queue in Home ›
**Requests** — filter by type, search, then **Approve** or **Reject** with an optional note; the requester
is notified and sees the outcome under **My requests** (also in the Chat panel's Requests tab).

Approving is a decision, not an edit: the ADMIN/PM then makes the change in the library as usual.

## Jobs a checklist can gate

| Job | When the gate appears |
| --- | --- |
| **Create project** | Pressing **Create** in the new-project wizard. |
| **AI spec review / compose / suggest** | Running those AI spec actions. |
| **Approve User Todo / User Q&A / AI Todo** | Approving rows in those books. |

## Running a gate

When a job has checklists, a dialog shows each one with its items and a **Pass / Fail / Skip** choice
per item:

- Set the verdicts by hand, or click **Ask AI** — a read-only AI evaluates the context (for example the
  spec) and fills them in.
- Each checklist shows its score against its minimum.
- **Confirm** records every run. The job continues only when **every** checklist meets its minimum and
  its required items pass; otherwise it's blocked and the dialog says why (the runs are still saved).

## Project checklists (project › Checklists tab)

A project starts **using the org defaults**. As soon as you change something, the project gets its own
set:

- **Attach** org checklists, **create** project-only ones, or **fork** an org checklist to edit a copy
  ("source has vN" shows when the original moves on; **Update from source** pulls it in).
- **Turn each one on or off** for this project.
- Override the **jobs**, the **minimum %** and the **version** used in this project.
- **Reset to org defaults** drops the project's own set.

The tab also lists every **checklist run** of the project. Editing needs the project's
checklist-manage permission (ADMIN/PM by default); every member except customers can view it.

## Checklists in rules

An [automation rule](./27-automation-rules.md) can **run a checklist with AI** (against the spec, a PR
diff or a task) and react when a run falls **below its minimum** — for example notify the PM.

## Limits

The number of checklists and how many versions are kept are set per organization by 4PM; the Checklists
panel shows how much of the cap is used.

See also: [Checklists FAQ](../faq/checklists.md).
