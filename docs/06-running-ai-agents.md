# Run AI agents & commands

Once a project is **ready**, you drive the AI and other tools from the dashboard. Every command
you dispatch runs on the worker through the project's machine-user CLI, and the output streams
back to your browser live.

## The Console tab

The project's **Console** is where you send commands and watch results. It has two sub-tabs:

- **Console** — type prompts/commands and see streamed output.
- **Commands** — the project's full command history, including commands you ran here **and**
  commands typed directly in the CLI on the worker. Each row shows an **origin** (`web` or
  `cli`); click a row to read the full text (Markdown and pretty-printed JSON).

## What you can dispatch

- **AI prompts** — send a prompt to `claude` (or the configured agent). Marked as AI work, it
  counts against quota and token limits.
- **Git operations** — see the dedicated [Git operations](./07-git-operations.md) doc.
- **Shell / tools** — allowed commands like `gh`, `glab`, and shell run on the worker.

Output streams back with **backpressure handling** — the CLI batches and flushes output
periodically so the browser stays responsive. Very large output may be truncated with a
`…(truncated)` marker.

## Live activity across tabs

Everyone in your org who has the project open sees a **live activity feed**: commands starting
and finishing in other tabs (for example, the Console and the Spec editor), each with a label.
You can click into a running command to watch its output — so a whole team can follow the AI
together in real time.

## Collapsible result blocks

AI results that come back as **JSON or code** are collapsed into a `▸[N]` marker to keep the
console readable:

- **On the web** — click the marker to open the block in a modal.
- **In the CLI (TUI)** — expand with the `/expand [N]` slash command.

Prose answers are shown as-is.

## AI spec-assist

The Suggest / Review / Compose buttons in the project wizard and the Spec tab are also AI
commands under the hood — they run on the same path, with the same quota and token accounting.
See [Create & manage projects](./05-projects.md#the-spec-and-ai-assist).

## Quota & limits

Before running an AI command, 4PM checks a few things:

- **Quota** — AI usage is metered to your organization and counts against your **plan's quota**.
  If you're out of quota, the command is refused; upgrade your plan or buy add-ons (see
  [Plans, billing & add-ons](./10-billing-and-plans.md)).
- **Per-prompt token limit** — if a prompt exceeds the project's per-prompt token limit, it is
  **not** run and you get a `PROMPT_TOKEN_LIMIT_EXCEEDED` error. Shorten the prompt or raise the
  limit.
- **Outbound review (if enabled)** — some projects require each AI input to be approved before it
  runs. If review is on and the input isn't approved (or no reviewer is available), the command is
  blocked and the PM is notified.

## Tips

- Give commands a clear intent; the activity feed and history are easier to follow with good
  labels.
- If a command seems stuck, check the machine-user status (it may be **offline** or **busy**) in
  the machines area.

See also: [AI commands FAQ](../faq/ai-commands.md).
