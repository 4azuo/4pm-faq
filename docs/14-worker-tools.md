# Worker tools

Your worker runs its work through command-line tools installed on the machine — the AI CLIs,
the Git tools, and the base toolchain. The **Tools** tab (on a machine-user's page) lets you
see which tools are present on a connected worker and install the missing ones **without
shelling into the machine**.

## The default tools

4PM knows about a default set of tools and checks each one on your worker:

| Tool | What it's for |
| --- | --- |
| **git** | Version control — clone, commit, push. |
| **node** | The JavaScript runtime the CLIs run on. |
| **npm** | Node's package manager (ships with Node). |
| **pnpm** | A faster alternative package manager. |
| **claude** | The Claude AI command-line agent. |
| **codex** | The Codex AI command-line agent. |
| **gh** | GitHub's official CLI (PRs, issues, releases). |
| **glab** | GitLab's official CLI. |

Each row shows whether the tool is **installed** and its **version**, or **not installed**.

## Installing & removing tools

- Tools distributed as packages — **pnpm**, **claude**, **codex**, and any other package you
  name — can be **installed** straight from the panel. Pick **npm** or **pnpm** as the
  installer and 4PM installs it **globally** on the worker so every project can use it.
- You can also **install any extra tool** by typing its package name — handy for a one-off tool
  your project needs.
- Installed packages can be **uninstalled** the same way.
- **git**, **node**, **npm**, **gh** and **glab** are **prerequisites** that come with the
  machine (or the operating system), so the panel shows their status with a short setup note
  rather than an install button — they aren't installed or removed through the package
  managers.

## Watching progress

Installing a tool can take a little while. The panel **streams the progress live** — you see
each line of output as it happens, and the row unlocks again when the install (or uninstall)
finishes.

## Who can do this

- The **Tools** tab is available for a machine-user that runs a CLI, only while the worker is
  **connected**; installing/uninstalling is limited to **managers** of the machine-user.
- For a **rented (4PM-hosted) machine-user**, the tools are managed by the 4PM team, so the
  panel isn't shown on your side — ask support if a rented worker is missing a tool.

## Tips

- If an AI command fails because a tool "isn't found", open Worker tools and check that the
  tool is installed and has a recent version.
- Prefer the default tools where possible — they're the ones 4PM tests against.

See also: [Worker tools FAQ](../faq/worker-tools.md) ·
[Run AI agents & commands](./06-running-ai-agents.md) ·
[Connect a worker](./03-connect-a-worker.md).
