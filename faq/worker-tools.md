# Worker tools

**Q: What are "worker tools"?**
The command-line tools installed on your worker machine that 4PM uses to do work — `git`,
`node`, `npm`, `pnpm`, the AI CLIs `claude` and `codex`, and the Git CLIs `gh` and `glab`. The
**Tools** tab on a machine-user's page shows which are installed and lets you install the
missing ones.

**Q: How do I see what's installed on my worker?**
Open the machine-user's **Tools** tab. Each tool shows **installed + version** or **not
installed**. The worker must be **connected**.

**Q: How do I install a missing tool?**
Click **Install** on the tool's row, or type a package name in the "install a package" field.
Choose **npm** or **pnpm** as the installer; 4PM installs it globally on the worker. You can
watch the install **progress stream live**.

**Q: Can I install a tool that isn't in the default list?**
Yes — type its package name and install it with npm or pnpm.

**Q: Can I remove a tool?**
Yes, use **Uninstall** on an installed package. The prerequisites `git`, `node`, `npm`, `gh`
and `glab` can't be removed from the panel — they come with the machine/OS.

**Q: A tool shows a setup note instead of an Install button — why?**
`git`, `node`, `npm`, `gh` and `glab` are installed with the machine or operating system, not
through npm/pnpm, so the panel shows their status and a short note on how to set them up.

**Q: My rented worker is missing a tool — what do I do?**
Rented (4PM-hosted) workers are managed by the 4PM team, so the Worker tools panel isn't shown
on your side. Contact support and mention which tool you need.

See also: [Worker tools](../docs/14-worker-tools.md).
