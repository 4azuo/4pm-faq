# AI commands & the console

**How do I run the AI on a project?**
Open the project's **Console** tab and dispatch a prompt. It runs on the worker via the project's
machine-user, and output streams back live. See [docs/06](../docs/06-running-ai-agents.md).

**Where do I see command history?**
The Console's **Commands** sub-tab lists every command for the project — from the web **and** from
the CLI on the worker — with an **origin** column (`web`/`cli`). Click a row to read the full
output.

**Can my teammates watch a command run?**
Yes. Everyone in your org with the project open sees a **live activity feed** of commands
starting/finishing across tabs, and can open a running command to watch its output.

**Why is an AI result collapsed into a `▸[N]` marker?**
JSON/code results are collapsed to keep the console readable. Click the marker on the web (opens a
modal) or use `/expand [N]` in the CLI. Prose answers are shown as-is.

**My prompt was refused with "PROMPT_TOKEN_LIMIT_EXCEEDED".**
The prompt exceeded the project's per-prompt token limit, so it wasn't run. Shorten the prompt or
raise the limit.

**"Waiting for an AI run slot — N ahead".**
Your org is at its plan's limit of parallel AI runs (Free 2, Pro 10, Max 30). The run starts
automatically; you can also stop it.

**My AI run stopped with a time-limit error.**
Single AI runs stop after the AI run time limit (300 s by default). Raise it in the project Settings or
the worker config.

**The AI says the session expired / out of credits.**
The worker's AI account is signed out or exhausted; it fails over to the next AI profile if there is
one. Sign the account in again with `4pm ai-login`, or add another profile — see
[worker configuration](../docs/21-worker-config.md).

**Can I attach screenshots or files to a prompt?**
Yes — 📎, paste or drag-and-drop (up to 10 files of 10 MB). Each becomes an `[Image#N]` / `[File#N]`
label the AI can see.

**Can I run `4pm` slash commands from the web?**
Yes — type `/` then Tab in the Console. `/quit` and `/config` are blocked from the web by default. See
the [CLI reference](../docs/20-cli-reference.md).

**My command was refused for quota.**
AI usage is metered to your org and counts against your **plan's quota**. Upgrade your plan or buy
a scale-pack add-on ([docs/10](../docs/10-billing-and-plans.md)).

**My push/AI input is "waiting for review" or blocked.**
The project has **outbound review** enabled — inputs must be approved before they run/leave the
worker. Get it approved, or ask the PM. If no reviewer is available it stays blocked.

**A command seems stuck.**
Check the machine-user status in the machines area — it may be **offline** or **busy**. Very large
output may also be truncated (`…(truncated)`), which is expected.

**Are the spec Suggest/Review/Compose buttons AI commands too?**
Yes — they run on the same dispatch path with the same quota and token accounting.
