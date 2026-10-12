# `4pm` CLI reference

All the commands, flags and in-terminal slash commands of the `4pm` worker CLI. To install it and
pair a machine, see [Install & run the CLI](./15-install-cli.md) and
[Connect a worker](./03-connect-a-worker.md).

## Commands

| Command | What it does |
| --- | --- |
| `4pm link` | **Pair** this machine with your 4PM server. Prints a pairing code to enter on the web (Machines › Register a machine), then asks for the confirmation code. Saves the credential in the profile. Running it again renews the pairing. |
| `4pm start` | **Run the worker**: checks for updates, connects to the server and waits for work. This is the long-running (headless) daemon. Needs a paired profile. |
| `4pm attach` | Open the interactive **terminal UI (TUI)** against a running `4pm start` daemon. Closing it leaves the daemon running. |
| `4pm ai-login` | Sign in the **AI CLIs** (Claude / Codex) of the worker's AI profiles, in place (for Claude, type `/login`). Use `--ai <dir or number>` to sign in only one profile. |
| `4pm auto-run` | Run **one autonomous cycle now** through the running daemon (normally the schedule does this). |
| `4pm unlink` | **Unpair**: revokes the link on the server and deletes the local credential. |
| `4pm version` | Show the installed version, and — if the server is reachable — the latest and the minimum supported version. |
| `4pm update` (or `upgrade`) | Update to the latest version now, even if auto-update is off. |
| `4pm credential-export` | Print the profile's identity as one value (`FOURPM_CREDENTIAL`) for a secret store — for containers without a persistent volume. |

Commands like `git-credential`, `git-token` and `net-connect` exist too, but they're used internally by
the worker — don't run them yourself.

## Flags

| Flag | Applies to | Meaning |
| --- | --- | --- |
| `--server <url>` | `link`, `version`, `update` | The 4PM server to talk to. `link` saves it, so later commands reuse it. |
| `--profile <name>` | every command | Act on a specific **profile** (an independent worker instance with its own credential and config). Normally not needed: `link` names the profile after the paired machine-user, and `start`/`unlink` show a picker when there are several. |
| `--token <token>` | `link` | Pair **headlessly** with a provisioning token instead of the code exchange. |
| `--ai <dir or number>` | `ai-login` | Sign in only that AI profile. |

## Environment variables

| Variable | Meaning |
| --- | --- |
| `FOURPM_SERVER` | Default server URL when `--server` isn't given. |
| `FOURPM_PROFILE` | Default profile (same as `--profile`). |
| `FOURPM_PAIR_TOKEN` | Provisioning token: a container started with it pairs itself on first boot (automated / pool deploys). |
| `FOURPM_CREDENTIAL` | A `credential-export` value: `4pm start` restores that identity when the profile has no credential yet — no re-pairing on ephemeral containers. |
| `FOURPM_ALLOW_INSECURE_TRANSPORT=1` | Allow a plain `http://` server — **local testing only**. |

## Profiles & files

- Each profile lives in `~/.4pm/profiles/<name>/`: the pairing credential (`.cre`), the worker config
  (`config.json`), logs, and the project working copy.
- One machine can run **several profiles at once** — one per project. Each profile has its own
  machine-user.
- In Docker, `~/.4pm` is the named volume (`4pm-home`), so pairing and work survive container
  re-creation.

## Slash commands (TUI and web Console)

In the TUI (`4pm attach`) — and from the project's web **Console** — type `/` then Tab to complete:

| Command | What it does |
| --- | --- |
| `/help` | List the slash commands. |
| `/version` | Show the CLI version. |
| `/status` | Connection, profile and session status. |
| `/whoami` | This machine account, its teams and projects. |
| `/history [N]` | The last N commands with times. |
| `/output <n>` | Replay a command's output (`n` from `/history`). |
| `/logs [N]` | Tail the profile's log. |
| `/expand [N]` · `/collapse [N]` | Expand / collapse a collapsed `▸[N]` result block. |
| `/reconnect` | Reconnect to the server now. |
| `/ai-profile [list \| use <n> \| reset]` | List the AI profiles, or choose which one runs (the others stay as fallback). |
| `/claude-cmd /context` | Run an AI-CLI slash command such as `/context`, `/usage`, `/status`. |
| `/config [show \| init \| set <k> <v> \| delete <k>]` | View or change the profile config. |
| `/clear` | Clear the transcript. |
| `/quit` | Quit the CLI (also `/exit`, Ctrl+C). |

From the **web** Console, `/quit` and `/config` are **blocked by default** (they would stop or tamper
with the worker). The worker's config decides which commands the web may run — see
[Worker configuration](./21-worker-config.md#console-settings).

## Updating

- **npm install:** the CLI updates itself when it starts (unless auto-update is off); `4pm update`
  forces it. Every profile on the machine uses the shared binary.
- **Docker:** pull a newer image and re-create the container. The **Full (locked)** image never updates
  itself.
- From the web you can update a worker (**Update** on a machine-user), a pool, or **Update all CLIs**.
  Workers running autonomous mode, rented workers and locked-image workers are skipped.
- A CLI older than the **minimum supported** version is refused when it connects; the web shows the
  version in red (too old) or amber (update available).

See also: [CLI & worker config FAQ](../faq/cli-and-worker-config.md).
