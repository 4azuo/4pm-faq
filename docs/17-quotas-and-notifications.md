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

Setting quotas needs the quota-manage permission; viewing needs quota-read. If you can't see or
edit the screen, ask an ADMIN.

## Notification center

The **Notifications** screen is your inbox — open it from the **bell** in the header. It lists
your notifications with their **type**, **content**, **time** and **read/unread** status.

- **Mark one** notification as read, or **Read all** from the toolbar.
- New notifications also surface as a **badge/toast** on any screen in real time (the same channel
  that streams job progress), so you don't have to keep the page open.

Typical notifications: a background job (project create/add) finishing, an approval you need to
make, a support reply, a usage alert, or a billing/payment event.

See also: [Notifications & quotas FAQ](../faq/quotas-and-notifications.md) ·
[Plans, billing & add-ons](./10-billing-and-plans.md).
