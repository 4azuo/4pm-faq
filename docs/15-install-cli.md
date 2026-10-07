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

- **Node.js ≥ 20** on the worker (`node -v`).
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
docker pull ghcr.io/4azuo/4pm-cli:full     # "full" bundles the toolchain (claude/codex/gh/glab/git)
# ghcr.io/4azuo/4pm-cli:latest              # base image (cli only) if you bring your own tools
```

**2. Pair once** (interactive — enter the hashcode from the web `/machines` page). State lives in
a named volume, so it survives restarts:

```bash
docker run --rm -it -e FOURPM_SERVER=https://<your-server-url> \
  -v 4pm-home:/home/node/.4pm ghcr.io/4azuo/4pm-cli:full link
```

**3. Sign in to the AI CLI + git hosts** (the agent can't run until the AI CLI is signed in):

```bash
docker exec -it 4pm-cli 4pm ai-login      # claude / codex sign-in
docker exec -it 4pm-cli gh auth login     # + glab auth login if you use GitLab
```

**4. Run the headless worker** (observe it from the web Console):

```bash
docker run -d --restart=unless-stopped --name 4pm-cli \
  -e FOURPM_SERVER=https://<your-server-url> \
  -v 4pm-home:/home/node/.4pm ghcr.io/4azuo/4pm-cli:full
```

The **Customize** button on the `/cli` page composes this run line for you — options include
*pull the latest image*, *recreate the container* safely (the credential/state lives in the
volume, not the container), and read-only mounts of your host's `claude`/`codex`/`gh`/`glab`
credentials.

**Attach a terminal, stop, resume:**

```bash
docker exec -it 4pm-cli 4pm attach   # attach a TUI to the running daemon
docker stop 4pm-cli                  # stop — credentials/state stay in the volume
docker start 4pm-cli                 # resume where it left off
```

To pick up a new CLI version in Docker, `docker pull` the newer tag and recreate the container
(the in-process auto-update doesn't apply in a container).

> **Update = pull + recreate.** Because the credential and cloned project live in the `4pm-home`
> volume (not the container), recreating the container never loses your pairing or work.

---

## After it's running

Once paired and connected, the CLI's **machine-user** appears under the machines area as **idle**
(paired, not yet serving a project). Attach it to a project to start dispatching work — see
[Machine-users & workers](./04-machine-users-and-workers.md) and
[Create & manage projects](./05-projects.md).

Don't want to run your own worker at all? **Rent a 4PM-operated machine-user** — see
[Rent a 4PM machine-user](./11-rented-machines.md).

See also: [Connect a worker (pairing)](./03-connect-a-worker.md) ·
[Install & Docker FAQ](../faq/install-cli.md).
