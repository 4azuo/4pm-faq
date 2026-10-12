# CLI commands & worker configuration

**What commands does the `4pm` CLI have?**
`link` (pair), `start` (run the worker), `attach` (open a terminal UI on a running worker), `ai-login`
(sign in Claude/Codex), `auto-run` (one autonomous cycle now), `unlink`, `version`, `update`, and
`credential-export`. Full list with flags: [docs/20](../docs/20-cli-reference.md).

**How do I point the CLI at my server?**
`4pm link --server https://<your-server>` — the server is saved with the pairing, so `start`, `version`
and `update` reuse it. Or set `FOURPM_SERVER`.

**How do I run several workers on one machine?**
Give each its own profile: `4pm --profile a link …` then `4pm --profile a start`. In Docker, use one
container and volume per worker (the `/cli` page names them after the account).

**Can a worker pair itself without typing codes?**
Yes — start the container with `FOURPM_PAIR_TOKEN=<token>` and it pairs on first boot. For containers
without a persistent volume, store `4pm credential-export` output in a secret store and pass it as
`FOURPM_CREDENTIAL`.

**Which slash commands work in the web Console?**
The same as the TUI (`/status`, `/history`, `/logs`, `/ai-profile`, `/claude-cmd /usage`…), except
`/quit` and `/config`, which are blocked from the web by default. The worker config decides which are
blocked.

**Where do I change a worker's settings?**
On the machine-user's page › **Settings** › **Worker configs** (the worker must be connected), or for many
workers at once with a template in **Machines › Configs**. See [docs/21](../docs/21-worker-config.md).

**How do I add a second AI account so runs don't stop at the limit?**
Add another **AI profile** (its own profile directory), sign it in with `4pm ai-login` (or mount the
login), and drag to set the order. When one account is out of credits or over its limit, runs fail over
to the next.

**"Two profiles use the same profile directory" — why can't I save?**
Each profile must point to its own directory; two profiles on one directory are the same account.

**How do I switch which AI account runs?**
In the Console, `/ai-profile` lists the profiles and `/ai-profile use N` makes one active (the others
remain fallbacks). `/ai-profile reset` goes back to normal.

**Can I use an Anthropic API key instead of a login?**
Yes — on a Claude profile set the **API key**: stored in 4PM (write-only), or read from AWS SSM
Parameter Store or Secrets Manager.

**How do I pick the model?**
Per AI profile in the worker config (a list of models the worker's CLI supports). A project can also set
its default model in the spec's AI guide section.

**My AI runs stop after 5 minutes.**
That's the **AI run time limit** (300 s by default). Raise it in the worker config, or per project in
Settings. Autonomous runs have their own **agent run timeout** (60 min).

**What's the difference between the `full`, `full-locked` and `base` images?**
`full` bundles claude/codex/gh/glab/git and updates itself; `full-locked` is the same but never updates
itself (pull a newer image to upgrade); `base` is the CLI only — install the AI CLIs from Worker tools.

**Why is my worker's Update button disabled with a "Locked" tag?**
It runs the `full-locked` image. Pull a newer image and re-create the container.

**What does "Agent user separation" do?**
The AI and project commands run as a separate user that can't read the worker's credential, config or
secrets, and network rules can be enforced. Keep it on (the default).

**Can I reuse the Claude/Codex login from my own machine?**
Yes — in the `/cli` page's Customize, **Mount claude/codex login**, one host folder per line. Each is
added as an AI profile. With agent separation on, it's copied into the container; your files aren't
changed.

**What setup do you recommend?**
See [Recommended setup](../docs/22-recommended-setup.md).
