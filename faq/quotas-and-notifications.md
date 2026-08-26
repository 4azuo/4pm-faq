# Quotas, usage & notifications

**What's the Quotas screen for?**
On top of your plan's overall quota, an **ADMIN/PM** can set **finer-grained quotas** per
organization, project, user or worker — each a metric with a limit, period and on-exceed action —
and view aggregated usage. See [docs/17](../docs/17-quotas-and-notifications.md).

**How is a quota enforced?**
4PM checks it **before** running an AI command; if a limit is reached, the command is refused per
the on-exceed action. Assigning a plan also auto-generates that plan's baseline quotas.

**I can't see or edit the Quotas screen.**
Viewing needs the quota-read permission and editing needs quota-manage — ask an ADMIN if you need
access.

**Where are my notifications?**
The **Notification center** (the **bell** in the header) lists your notifications with type,
content, time and read/unread status. See [docs/17](../docs/17-quotas-and-notifications.md#notification-center).

**How do I clear notifications?**
Mark one as read, or use **Read all**. New notifications also pop up as a **badge/toast** on any
screen in real time, so you don't need to keep the page open.

**What shows up as a notification?**
Things like a background job (project create/add) finishing, an approval you need to make, a
support reply, a usage alert, or a billing/payment event.

See also: [Quotas, usage & notifications](../docs/17-quotas-and-notifications.md) ·
[Run AI agents](../docs/06-running-ai-agents.md#quota--limits).
