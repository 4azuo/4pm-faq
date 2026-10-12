# Public API & API clients

Your own scripts and external systems (an ERP, a CI job, an internal portal) can drive 4PM through the
public API: users, teams, projects, memos, checklists, automation rules, autonomous mode, documents and
usage.

## How it works: a client acts as you

- **Anyone can create API clients** for themselves — every role except worker (machine) accounts,
  customers included.
- A client **acts as the person who created it** (its owner). It can only do what the owner is allowed to do,
  further limited to the **scopes** chosen for the client. A customer's client sees only the customer's
  projects; nobody's client can delete a project unless its owner could.
- **A client can never approve** anything — requests, tasks, answers, ER changes or network requests. It can
  post requests and answers, but a person still approves them in 4PM.
- What a client does is recorded under the owner's name, marked "via API: <client name>". The four-eyes rule
  applies to the owner: a request the owner's client posted can't be approved by the owner.
- If the owner is paused, removed or loses a permission, the client loses it too — within about a minute.

## Create a client

1. Open your **profile › Settings › API clients** and click **New client**.
2. Give it a name, choose its **scopes** and, optionally, an **IP allowlist**.
3. Confirm with your **password** (or, for a Google/GitHub-only account, an authenticator or recovery code).
4. Copy the **client ID** and **client secret** — the secret is shown **once**. Lost it? **Rotate** the secret
   (again with your password or code).

You can revoke, delete and view the activity of your clients there. **ADMINs** (and the root) also see every
client of the organization, with its owner, in **Organization Settings › API integrations**, and can revoke or
delete any of them.

## Scopes

| Scope | Allows |
| --- | --- |
| `users:read` / `users:write` | List and read users / create, update, pause, delete users |
| `teams:read` / `teams:write` | Read teams / manage teams and their members |
| `projects:read` / `projects:write` | Read projects, members and spec / create, update, manage members, pause, close |
| `memos:read` / `memos:write` | Read / manage project, team and personal memo items |
| `checklists:read` / `checklists:write` | Read checklists and runs / manage checklists, record runs, run a checklist with AI |
| `rules:read` / `rules:write` | Read rules, catalog and run log, dry-run / manage rules, retry runs, override org rules |
| `autonomous:read` / `autonomous:write` | Read status, settings, books, discussions / start, pause, change settings, post requests and answers, discuss, ask to approve |
| `documents:read` / `documents:write` | Read doc types and documents / generate documents |
| `usage:read` | Read quotas and usage |

A scope only opens the door: the owner still needs the matching permission in 4PM (for example, org rules need
an ADMIN, project rules the project's PM).

## Call the API

1. Get a token: `POST /oauth/token` with `grant_type=client_credentials`, your `client_id` and `client_secret`
   (in the body or as HTTP Basic auth), optionally a subset of `scope`. The token lasts about 15 minutes.
2. Call the `v1` endpoints with `Authorization: Bearer <token>`.
3. Errors come back as `{ error, error_description, code?, request_id }` — `code` is 4PM's own error code (for
   example `BOOK_CONFLICT`) when there is one.

Each call is checked against the token's scopes, the client's IP allowlist, a rate limit, the owner's
permissions and the owner's (and organization's) IP allowlists, and is audited.

## Long-running work: runs

Generating a document and running a checklist with AI take time. Those calls answer **202** with a **run**:

- Poll `GET /v1/projects/{id}/runs/{runId}` — status `queued`, `running`, `succeeded` or `failed`; when it
  succeeds, `result.artifactId` is the document or `result.checklistRunId` the checklist run.
- Or have an [automation rule](./27-automation-rules.md) with a **webhook** action push the outcome (triggers
  "A document was generated" or "A checklist run completed").

Runs use your organization's run slots and AI quota, like runs started in the app.

## Not available through the API

Approving anything, free Console prompts, secrets, network and agent-tool policies, git write operations,
billing, and permission grants. AI Verify on the books is planned.

## Run autonomous mode now

`POST /v1/projects/{id}/autonomous/run` (scope `autonomous:write`) runs one autonomous cycle right away instead of
waiting for the schedule — useful right after your system posted a request that a person approved. The cycle's
own rules still apply: nothing happens while autonomous mode is paused or in quiet hours, and only approved work
runs. The worker needs an up-to-date CLI.

## Reference

The full reference — every endpoint with its fields, sample requests and code in cURL, JavaScript, Python, Go,
Java and C# — is at **`/developers/api`** (the **API docs** button next to your API clients, or the footer
link).

See also: [Public API FAQ](../faq/public-api.md) · [Teams, members & permissions](./18-teams-and-permissions.md).
