# Run AI agents & commands

Once a project is **ready**, you drive the AI and other tools from the dashboard. Every command
you dispatch runs on the worker through the project's machine-user CLI, and the output streams
back to your browser live.

## The Console tab

The project's **Console** is where you send commands and watch results. Pick the machine-user to
talk to in its header. Sub-tabs:

- **Console** — type prompts/commands and see streamed output. Each AI run shows its start time and
  processing time; click the AI CLI name on a run to see the exact prompt and settings it ran with.
- **Commands** — the project's full command history, including commands you ran here **and**
  commands typed directly in the CLI on the worker. Each row shows an **origin** (`web` or
  `cli`) and the machine-user that ran it; click a row to read the full text (Markdown and
  pretty-printed JSON).
- **Memory** — what the shared AI memory remembers for a machine-user (when enabled), with a Clear
  button.
- **Tools** — the worker's tool versions (see [Worker tools](./14-worker-tools.md)).

## What you can dispatch

- **AI prompts** — send a prompt to `claude` (or the configured agent). Marked as AI work, it
  counts against quota and token limits.
- **Git operations** — see the dedicated [Git operations](./07-git-operations.md) doc.
- **Shell / tools** — allowed commands like `gh`, `glab`, and shell run on the worker.
- **`4pm` slash commands** — `/status`, `/history`, `/ai-profile`, `/claude-cmd /usage`… (type `/` then
  Tab to complete). `/quit` and `/config` are blocked from the web by default. See the
  [CLI reference](./20-cli-reference.md#slash-commands-tui-and-web-console).

**Attachments:** add images and files (PDF, Office, text, CSV, JSON, ZIP — up to 10 files of 10 MB) with
📎, paste or drag-and-drop. Each becomes an `[Image#N]` / `[File#N]` label the AI can see. A project
setting can block image attachments.

**AI settings:** the AI settings button sets the model, thinking level and temperature for the runs you
start from this tab (remembered in your browser; blank = the worker's defaults).

**Conversations:** a prompt continues the previous AI conversation only while it's recent and small;
otherwise a fresh one starts (from the shared memory, if enabled) — this keeps token use down. See
[Worker configuration](./21-worker-config.md#console-settings).

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

- **Run slots** — your plan sets how many AI runs can run at once across the organization (Free 2,
  Pro 10, Max 30). Extra runs **wait in a queue** and start automatically; the Console shows the queue
  position. You can **stop** a queued or running run.
- **Time limit** — a single AI run stops after the worker's / project's AI run time limit (300 s by
  default) with a clear error. Raise it in the project Settings or the worker config for long tasks.
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
  the machines area. A run whose worker disconnects stops with an error so you can re-run it.
- When an AI run fails, the Console shows the AI CLI's actual error (session expired, out of credits,
  timed out…). The worker fails over to its next AI account automatically when one is unavailable.

See also: [AI commands FAQ](../faq/ai-commands.md).
