# Quotas, usage & notifications

Two everyday screens: **Quotas & usage** (managers set caps and everyone can see consumption) and
the **Notification center** (your inbox of what happened).

## Quotas & usage

Your **plan** sets your organization's overall quota and caps (see
[Plans, billing & add-ons](./10-billing-and-plans.md)). On top of that, an **ADMIN/PM** can set
**finer-grained quotas** on the Quotas screen — per organization, project, user or worker.

- Each quota is a **metric** (e.g. AI usage) with a **limit**, a **period**, and an **on-exceed**
  action.
- The screen also shows **aggregated usage** (metric × period × total) so you can see how close
  you are to a limit.
- 4PM checks the quota **before** running an AI command; if a limit is hit, the command is refused
  (see [Run AI agents](./06-running-ai-agents.md#quota--limits)).
- Assigning a plan **auto-generates** the baseline quotas for that plan.

Beyond the basic quotas you can set **per-project and per-machine token and command limits**, command
budgets and **usage alerts** (monthly AI token alerts and project usage alerts, in-app or by email —
Pro plan and above). A project's **token budget bar** counts usage up to the minute. Usage reports can be
exported as **PDF** or **Excel**.

**Plan limits** (users, projects, storage, memo items, autonomous rows, rules…) are listed with your
current usage on the **Usage** tab.

Setting quotas needs the quota-manage permission; viewing needs quota-read. If you can't see or
edit the screen, ask an ADMIN.

## Storage

**Organization Settings › Storage** shows storage by content type (messages, command history, files,
4rum posts, memos, attachments, templates…). You can clear content by type and date (permanently), set
storage alerts, and turn on **auto clear** to delete the oldest content when storage fills up. When storage
is **full**, posting, messaging, uploads and new AI runs pause until you free space; ADMINs see a warning
from 90%.

## Notification center

The **Notifications** screen is your inbox — open it from the **bell** in the header. It lists
your notifications with their **type**, **content**, **time** and **read/unread** status.

- **Mark one** notification as read, or **Read all** from the toolbar.
- New notifications also surface as a **badge/toast** on any screen in real time (the same channel
  that streams job progress), so you don't have to keep the page open.

Typical notifications: a background job (project create/add) finishing, an approval you're asked to
make, a discussion mention or reply, an autonomous problem or question, a rule's notification, a
support reply, a usage alert, an announcement, or a billing/payment event. Some (approval requests,
announcements) also arrive by **email**.

See also: [Notifications & quotas FAQ](../faq/quotas-and-notifications.md) ·
[Plans, billing & add-ons](./10-billing-and-plans.md).
