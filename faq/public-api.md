# Public API & API clients

**Who can create an API client?**
Every user except worker (machine) accounts — including customers. Create it in your **profile › Settings ›
API clients**. See [docs/32](../docs/32-public-api.md).

**What can my client do?**
Only what **you** can do, limited to the scopes you gave it. It acts as you: what it does shows in History
under your name, marked "via API".

**Can a customer delete a project through the API?**
No. A customer's client has the customer's permissions — read their projects, post requests and answer AI
questions — and no scope can widen that.

**Can the API approve requests or tasks?**
No, never — not even for an ADMIN's client. It can post requests and answers and ask people to approve; a
person approves in 4PM.

**Why do I have to type my password to create a client?**
Creating a client or rotating its secret is sensitive, so you confirm it's you: your password, or an
authenticator / recovery code if you sign in only with Google or GitHub.

**I lost the client secret.**
It's shown only once. **Rotate** the secret (with your password or code) and update your system.

**My call returns 403 `forbidden` although the scope is right.**
The client's owner lacks the permission for that action (for example, only the project's PM may manage
project rules), or the action is never available through the API (approvals, secrets…).

**My call returns 403 from an unexpected IP.**
The client's IP allowlist — and your own account's and organization's IP allowlists — are checked against
the address your system calls from.

**How do I get the result of a document generation or a checklist AI run?**
They answer 202 with a run. Poll `GET /v1/projects/{id}/runs/{runId}` until it succeeds, or have an automation
rule with a webhook action notify your system.

**Can I trigger autonomous mode right away?**
Yes — `POST /v1/projects/{id}/autonomous/run` runs one cycle now (scope `autonomous:write`). It still does nothing while
paused or in quiet hours, and only approved work runs.

**Who can see and revoke all clients?**
ADMINs and the root, in **Organization Settings › API integrations** (with each client's owner). Everyone else
sees only their own.

**What happens to my clients if I leave or am paused?**
They stop working within about a minute — a client can never do more than its owner.

**Where is the reference?**
At `/developers/api` (the **API docs** button next to your API clients, or the footer).
