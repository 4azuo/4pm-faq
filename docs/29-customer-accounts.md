# Customer accounts (CLIENT role)

Invite your **customer** into the projects you build for them. A customer account (role **CLIENT**)
sees only the projects it's invited to — mostly read-only — and can post requests, answer the AI's
questions, take part in discussions and approve work when you ask it to. It never sees your team's
other projects, people or settings.

## Inviting a customer

1. Open the project › **Members** tab › **Invite a customer** (or the Invite dialog in user management
   with the **Customer (CLIENT)** role and at least one project).
2. The customer receives an email invitation, sets a username and password, and lands in the project.

Who can invite: ADMINs, and the PM of each project the customer is invited to. CLIENT is an exclusive
role — it can't be combined with other roles, added to or removed from an existing user later, put in a
team, or made a PM, team lead or worker. Customers appear with a **Customer** badge in member lists.

## What a customer sees

| Area | Customer access |
| --- | --- |
| Navigation | Only **Projects** (their projects), **Notifications** and their own profile. No search, AI Help, chat, community, memo or marketplace. |
| Dashboard | The project's info panel. |
| Spec | Read-only. |
| Generators | Documents of the doc types you allow customers to view — read-only. |
| Content › Files | Read-only. Git internals and **every git-ignored file** (e.g. `.env`, local credentials) are hidden. |
| Content › Git | History, read-only — no branches, commits, PRs or configuration. |
| Books | **User Todo**: post requests (and edit their own). **User Q&A**: answer the AI's questions. **AI Todo / AI Done**: read. |
| Discussions | Open, reply to and resolve their own discussions. |

Not available to customers: Console, Memo, Community, Usage, History, Settings, Checklists, Rules, worker
actions, and any AI action.

## Customers in your workflow

- **Requests & answers** from customers carry a **Customer** badge; sort or filter **Customer first** in the
  grids. Customer-posted requests still need approval by your team before the AI acts on them.
- **Customer approval:** in the project's **Approvals** tab you can require the **customer** to approve
  requests or tasks (per team and per book), and use **Ask to approve** to notify them by email.
- **Discussions** opened by customers are highlighted. Link one to a row to hold its approval until it's
  resolved.
- **Notifications:** customers get only what concerns them — approval requests, discussion mentions,
  replies and resolutions, and their requests being approved — in-app and by email. Internal events
  (autonomous alerts, quota, lifecycle…) are never sent to them.

## Permissions

A customer's permissions are fixed: read their projects and their Git history, and write their own book
rows. **No grant can widen a customer** — the Permissions tab lists only the permissions that apply.

## Tips

- Keep secrets out of tracked files: a customer can read any tracked file in the repo.
- Use **doc types' view access** to choose which generated documents (proposals, estimates, reports) the
  customer can read.
- Turn on a **customer approval** policy for requests that change scope or cost.

See also: [Customer accounts FAQ](../faq/customer-accounts.md) ·
[Task books & approvals](./28-task-books-and-approvals.md).
