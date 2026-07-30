# Connect a worker (pair the CLI)

To let 4PM run AI and Git on your machine, you install the **`4pm` CLI** on that machine (the
"worker") and **pair** it with your account. Pairing is a one-time secure handshake using three
hashcodes.

## Before you start

- You must be **logged in on the web**.
- Install the `4pm` CLI on the worker (it auto-updates itself on startup).
- The worker needs the tools you plan to use available on its PATH — e.g. `git`, `gh`/`glab`,
  and `claude` — authenticated as needed.

## Pairing, step by step

Pairing links one CLI to one machine-user via a **1 → 2 → 3 hashcode chain**:

```
1. Log in on the web.
2. Run the 4pm CLI for the first time  ─▶ it shows hashcode (1).
3. On the web, enter hashcode (1)       ─▶ the server returns hashcode (2).
4. In the CLI, enter hashcode (2)        ─▶ confirms the pairing (sends the machine fingerprint).
5. The server returns hashcode (3)       ─▶ the CLI saves it as its credential (.cre file).
```

- **Hashcode (3) is the link certificate** — a long random secret the CLI stores locally. The
  server never stores it in readable form; it only keeps a one-way hash to look the machine up.
- The pairing can be **permanent or time-limited** (an ADMIN/PM decides the lifetime).
- After pairing, the CLI opens a **secure, per-message-encrypted** connection to the server so
  commands and output flow safely.

## One machine, many CLIs

- A single worker machine can run **several CLIs in parallel**. Each CLI has its own profile,
  its own machine-user, and serves **one project** at a time.
- The server matches CLIs to a **worker** using the machine fingerprint captured during pairing.

## Re-pairing & 1:1 rule

- A machine-user is linked to exactly **one** CLI. If you pair the same machine-user to a
  **different** CLI, the old certificate is revoked and the old CLI logs out (closes its
  connection and deletes its credential).
- To move a project's worker to a new machine, re-pair its machine-user there.

## After pairing

Once a CLI is paired and connected, its **machine-user** shows up under the machines area of the
dashboard as **idle** (paired but not yet serving a project). You then attach it to a project —
see [Create & manage projects](./05-projects.md).

## Troubleshooting

- **Hashcode rejected / expired** — hashcodes are short-lived; restart the pairing and enter
  them promptly.
- **CLI won't connect after pairing** — check the worker's network/firewall and that the CLI is
  the latest version (it auto-updates on startup).
- **Old CLI got logged out** — expected if the same machine-user was paired elsewhere (1:1 rule).

See also: [Workers & pairing FAQ](../faq/workers-and-pairing.md).
