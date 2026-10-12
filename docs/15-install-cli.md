# Install & run the `4pm` CLI

The `4pm` CLI is the small app you run on a **worker** so 4PM can run AI and Git there. There
are **two ways** to run it — the same binary, two packaging modes — and the in-app **CLI** page
(`/cli`) shows copy-paste commands with your server URL and the current version already filled in:

- **Run directly** — install `@4pm/cli` straight on the machine and run it on the host. **No
  Docker, no sandbox.** Best for a personal worker or a dev machine.
- **Docker (headless)** — run the CLI as a container; the **container is the sandbox** that
  isolates the agent from the host. Best for isolation or cloud scale.

Either way the worker runs **headless** (a long-lived daemon you watch from the web Console), and
you can attach a terminal (TUI) to it when you want one. After installing, you **pair** it once —
see [Connect a worker](./03-connect-a-worker.md).

## Requirements

- **Node.js ≥ 24** on the worker (`node -v`) — only for the direct install; the Docker image ships its
  own Node.
- The tools you plan to use on the machine's `PATH` — typically `git`, `gh`/`glab`, and an AI CLI
  (`claude` / `codex`) — authenticated as needed. You can also install these later from the
  **Tools** tab — see [Worker tools](./14-worker-tools.md).
- **Windows:** run the CLI inside **WSL2 (Ubuntu)**, not native Windows — the AI toolchain expects
  a real Linux environment. Install WSL2 (`wsl --install -d Ubuntu`), install Node 24 inside
  Ubuntu, then follow the Linux steps below. (The Docker path uses Docker Desktop + WSL2.)

---

## Option 1 — Run directly (npm)

The simplest path when Node ≥ 24 is present:

```bash
npm i -g @4pm/cli     # install (public npm, no auth needed)
4pm --version         # check it installed
```

- **Auto-update:** installed this way, the CLI keeps itself up to date on startup — no extra
  config.
- **No npm on the machine?** Download the CLI **tarball** from the GitHub Release instead, verify
  the checksum shown on the `/cli` page, extract it and add its launcher to `PATH`. The `/cli`
  page gives the exact commands per OS.

Then pair and start:

```bash
4pm link --server https://<your-server-url>   # one-time pairing (see docs/03)
4pm start                                      # connect and wait for work
```

### Running several workers on one machine

One machine can run **several CLIs in parallel**, each serving its own project. Give each its own
**profile**:

```bash
4pm --profile a link --server https://<your-server-url>
4pm --profile a start
```

Each profile keeps its own pairing credential and config, preserved across auto-updates.

---

## Option 2 — Docker (headless)

Run the CLI as a container — the container **is** the sandbox. Everything runs with plain
`docker`; you don't need the source. Install a container runtime first (Docker Desktop + WSL2 on
Windows, Docker Desktop / colima on macOS, `get.docker.com` on Linux).

> **Docker or Podman?** The `/cli` page has a **Docker | Podman** toggle. Podman is
> command-line compatible — pick it and every command below swaps `docker` → `podman` (and, on
> localhost, `host.docker.internal` → `host.containers.internal`). The steps are otherwise
> identical, so the examples below use `docker`.

**1. Pull the image**

```bash
docker pull ghcr.io/4azuo/4pm-cli:full     # bundles the toolchain (claude/codex/gh/glab/git)
```

Three image variants — pick one on the `/cli` page's **Worker image** switch:

| Image | Contents | Updates |
| --- | --- | --- |
| `:full` | CLI + `claude`, `codex`, `gh`, `glab`, `git` — runs immediately. | The CLI updates itself. |
| `:full-locked` | Same as Full. | The CLI **never** updates itself; upgrade by pulling a newer image. Worker tools can still be installed/updated. The web shows a **Locked** tag. |
| `:base` | CLI only, lighter. | Install `claude`/`codex` from the Worker tools panel before the agent can run. |

**2. Pair once** (interactive — enter the hashcode from the web `/machines` page). State lives in
a named volume, so it survives restarts:

```bash
docker run --rm -it -e FOURPM_SERVER=https://<your-server-url> \
  -v 4pm-home:/home/node/.4pm ghcr.io/4azuo/4pm-cli:full link
```

**3. Run the headless worker** (observe it from the web Console):

```bash
docker run -d --init --restart=unless-stopped --name 4pm-cli \
  -e FOURPM_SERVER=https://<your-server-url> \
  -v 4pm-home:/home/node/.4pm ghcr.io/4azuo/4pm-cli:full
```

Copy the real line from the `/cli` page — its **Customize** button composes it with your options (see
below), including the security hardening that's on by default.

**4. Sign in to the AI CLI + git hosts** (the agent can't run until the AI CLI is signed in), unless
you mount your host's logins instead (below):

```bash
docker exec -it 4pm-cli 4pm ai-login      # claude / codex sign-in (claude: type /login)
docker exec -it 4pm-cli gh auth login     # + glab auth login if you use GitLab
```

Logins made this way are stored in the volume and survive re-creating the container.

### Customize the run command

| Option | Default | What it does |
| --- | --- | --- |
| **Pull the latest image first** | off | Prepends `docker pull`. |
| **Re-run (recreate the container)** | off | Removes the old container first — safe, state is in the volume. |
| **Agent user separation** | **on (recommended)** | AI CLIs and project commands run as a separate user that can't read the worker's identity, config or secrets. Also lets the worker enforce [network rules](./25-project-content.md#networks). |
| **Mount claude / codex login (host)** | off | Reuse your host's AI logins — **one folder per line** for several accounts. Each becomes an AI profile automatically. With separation on, the login is **copied** into the container (your host files are never changed). |
| **Mount gh / glab login (host)** | off | Reuse your host's GitHub/GitLab login for projects on *Self-managed* git auth. ⚠️ The agent can use that account's **full** permissions — mount a dedicated account. If the host keeps the token in a system keyring, log in with `gh auth login --insecure-storage` or inside the container. |
| **Resource limits** | blank | CPU, memory, swap, processes, `/dev/shm`. The Machines page warns when a worker has no limits or claims more than its host has. |
| **Read-only root filesystem**, **no new privileges**, **drop capabilities** | **on** | Hardened by default; the folders the worker needs stay writable. |
| **Allow insecure transport** | off | Allow a plain `http://` server — local testing only. |
| **Extra flags / args** | — | Free-form `docker run` flags (before the image) or container args (after it). |

**Permission denied on the volume?** A reused root-owned volume or host folder needs a one-time fix —
the CLI runs as the non-root `node` user (uid 1000): `sudo chown -R 1000:1000 <host-path>`.

### Automated and ephemeral workers

- **Headless pairing:** start the container with `-e FOURPM_PAIR_TOKEN=<token>` and it pairs itself on
  first boot — no interactive code exchange (for automated / pool deploys).
- **No persistent volume** (e.g. a cloud task): run `4pm credential-export` once on a paired worker, store
  the value in a secret store, and pass it as `FOURPM_CREDENTIAL` — the worker restores the same identity
  on every boot without re-pairing.

**Attach a terminal, stop, resume:**

```bash
docker exec -it 4pm-cli 4pm attach   # attach a TUI to the running daemon
docker stop 4pm-cli                  # stop — credentials/state stay in the volume
docker start 4pm-cli                 # resume where it left off
```

To pick up a new CLI version on the **locked** image, `docker pull` the newer tag and recreate the
container. The `:full` and `:base` images can also update from the web.

> **Recreating is safe.** Because the credential and cloned project live in the `4pm-home` volume (not
> the container), pulling a new image and recreating the container never loses your pairing or work.

---

## After it's running

Once paired and connected, the CLI's **machine-user** appears under the machines area as **idle**
(paired, not yet serving a project). Attach it to a project to start dispatching work — see
[Machine-users & workers](./04-machine-users-and-workers.md) and
[Create & manage projects](./05-projects.md).

Not sure which options to pick? See [Recommended setup](./22-recommended-setup.md). All commands and
flags: [CLI reference](./20-cli-reference.md).

Don't want to run your own worker at all? **Rent a 4PM-operated machine-user** — see
[Rent a 4PM machine-user](./11-rented-machines.md).

See also: [Connect a worker (pairing)](./03-connect-a-worker.md) ·
[Install & Docker FAQ](../faq/install-cli.md).
