# Customer accounts (CLIENT)

**How do I give my customer access to a project?**
Project › **Members** › **Invite a customer**. They get an email, set a username and password, and see only
the projects they're invited to. See [docs/29](../docs/29-customer-accounts.md).

**What can a customer see and do?**
Read the project overview, spec, allowed documents, files and Git history; **post requests** (User Todo),
**answer the AI's questions** (User Q&A), read AI Todo and AI Done, and take part in **discussions**. No
Console, settings, other projects or people.

**Can a customer see my `.env` or secrets?**
Not git-ignored files — those are hidden from customers. Any **tracked** file in the repo is visible, so
don't commit secrets.

**Can I give a customer more permissions?**
No. A customer's permissions are fixed and no grant can widen them.

**Can a customer approve work?**
Yes, if you require it: in the **Approvals** tab, add the customer as a required approver for a team or
book, then use **Ask to approve**.

**Can I turn an existing member into a customer (or back)?**
No — the CLIENT role is set at invitation and can't be added or removed later. Invite a new customer
account instead.

**What notifications does a customer get?**
Only approval requests, discussion mentions/replies/resolutions and their approved requests — in-app and
by email. Internal alerts are never sent to customers.

**How do I spot customer requests?**
They carry a **Customer** badge; use **Customer first** to sort or filter the grids.
