# Installing & running the CLI

**How do I install the `4pm` CLI?**
The quickest way, with **Node ≥ 20** on the machine, is npm: `npm i -g @4pm/cli`, then
`4pm --version`. No npm? Download the release tarball, verify the checksum shown on the `/cli`
page, and run it. Full steps: [docs/15](../docs/15-install-cli.md).

**Where do I get the exact commands?**
The in-app **CLI** page (`/cli`) shows copy-paste commands for each OS with your **server URL** and
the current **version** already filled in — for both the direct install and Docker.

**Do I need Docker?**
No. **Run directly** (npm/tarball) on the host, or use **Docker (headless)** where the container is
the sandbox. Direct is simplest for a personal/dev machine; Docker isolates the agent from the
host. See [docs/15](../docs/15-install-cli.md).

**How do I run it in Docker (headless)?**
Pull `ghcr.io/4azuo/4pm-cli:full`, pair once (`docker run … link`), sign in the AI CLI with
`docker exec -it 4pm-cli 4pm ai-login` (plus `gh`/`glab auth login`), then run detached:
`docker run -d --restart=unless-stopped --name 4pm-cli -e FOURPM_SERVER=… -v 4pm-home:/home/node/.4pm ghcr.io/4azuo/4pm-cli:full`.
The `/cli` page's **Customize** button builds this line for you. Detail:
[docs/15 — Docker](../docs/15-install-cli.md#option-2--docker-headless).

**Can I use Podman instead of Docker?**
Yes. The `/cli` page has a **Docker | Podman** toggle — Podman is command-line compatible, so the
same commands run with `podman` (on localhost it uses `host.containers.internal` instead of
`host.docker.internal`). See [docs/15](../docs/15-install-cli.md#option-2--docker-headless).

**What's the difference between the `full` and base images?**
`:full` bundles the toolchain (`claude`/`codex`/`gh`/`glab`/`git`); `:latest` (base) is the CLI
only, for when you bring your own tools.

**How do I sign in to Claude/Codex and GitHub inside the container?**
`4pm ai-login` handles the AI CLI sign-in; `gh auth login` / `glab auth login` handle the git
hosts. The agent can't run until the AI CLI is signed in. (Running directly, you authenticate
`claude`/`codex`/`gh`/`glab` on the host as usual.)

**Can I get a terminal on a headless worker?**
Yes — attach a TUI to the running daemon: `docker exec -it 4pm-cli 4pm attach` (or `4pm attach`
when running directly). Detaching leaves the daemon running.

**How do I update the CLI?**
Installed via npm, it **auto-updates on startup**. In Docker, `docker pull` the newer tag and
recreate the container — your pairing and cloned project live in the `4pm-home` volume, so nothing
is lost.

**I'm on Windows.**
Run the CLI inside **WSL2 (Ubuntu)** — the AI toolchain expects a real Linux environment. Install
WSL2 (`wsl --install -d Ubuntu`) + Node 20 inside Ubuntu, then use the Linux steps. The Docker path
uses Docker Desktop + WSL2.

**Can one machine run several workers?**
Yes — run several CLIs, each with its own **profile**: `4pm --profile a link …` then
`4pm --profile a start`. Each serves one project.

**`4pm: command not found` after installing.**
Open a new terminal so the updated `PATH` takes effect. If you installed the tarball, make sure its
launcher directory is on `PATH`.

See also: [Install & run the CLI](../docs/15-install-cli.md) ·
[Connect a worker](../docs/03-connect-a-worker.md) · [Worker tools](../docs/14-worker-tools.md).
