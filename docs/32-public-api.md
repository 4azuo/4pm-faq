# Public API & OAuth clients

External systems (your HR tool, an internal portal, a provisioning script) can manage your
organization's **users**, **projects** and **teams** through 4PM's public integration API.

## Create an API client

1. As the organization's **root** user, open **Organization Settings › API integrations**.
2. **New client**: give it a name, choose its **scopes** (`users`, `projects`, `teams`), and optionally an
   **IP allowlist**.
3. Copy the **client secret** — it's shown **once**. Lost it? **Rotate** to get a new one.

You can also **revoke** a client and view its **activity log**.

## Call the API

1. Request a token: `POST /oauth/token` with `grant_type=client_credentials`, your `client_id` and
   `client_secret` (in the body or as HTTP Basic authentication), and optionally a subset of `scope`.
2. You get a short-lived bearer token (about 15 minutes).
3. Call the `v1` endpoints with `Authorization: Bearer <token>` — for example list users (by role),
   create a project (with a team and a group), list projects by team, create or update a team and its
   members.

Each call is checked against the token's scope, the client's IP allowlist and a rate limit, and is
audited.

## Reference

The full reference — every endpoint with its URL, request and response format, error codes, and sample
code in cURL, JavaScript, Python, Go, Java and C# — is at **`/developers/api`** (the **API docs** button in
Settings › API integrations, or the footer link).

See also: [Teams, members & permissions](./18-teams-and-permissions.md).
