# Checklists

**What is a checklist?**
A reusable, versioned list of items to check before an action. Bound to a job (Create project, AI spec
review/compose/suggest, approving User Todo / User Q&A / AI Todo), it acts as a **gate**. See
[docs/26](../docs/26-checklists.md).

**Where do I manage them?**
Organization checklists: Home › **Checklists** (ADMIN/PM). Per project: the project's **Checklists** tab.

**Why was my action blocked by a checklist?**
A bound checklist scored below its **minimum %**, or a **required** item didn't pass. The dialog shows
which. Fix the cause and run it again, or ask a manager to adjust the checklist. A minimum of 0 % is
advisory and never blocks.

**Can the AI fill in the checklist?**
Yes — click **Ask AI** in the gate dialog: a read-only AI evaluates the context (e.g. the spec) and sets
each item. You can change its verdicts before confirming.

**Can a project use different checklists from the org?**
Yes. In the project's Checklists tab, attach org checklists, create project-only ones or fork an org one,
turn each on or off, and override its jobs, minimum % and version. **Reset to org defaults** undoes it.

**Can the AI write the checklist items for me?**
Yes — **AI authoring**: describe what to add or change, review the AI's draft, and save it as a new
version.

**I can't edit the org library.**
Only ADMINs and PMs edit it. Click **Request a change** on the checklist; they review it in Home ›
Requests and reply with a note. Approving doesn't edit anything by itself — they then make the change.
Track your requests under **My requests** or in the Chat panel's Requests tab.

**Where do I see past runs?**
Each checklist's detail lists its runs (version, who ran it — person or AI — per-item results and score),
and the project's Checklists tab lists all runs of that project.
