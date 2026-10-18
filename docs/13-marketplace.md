# Marketplace & knowledge hub

4PM has a built-in **marketplace** for reusable agent building blocks — **skills**, **subagents**,
**Claude commands**, **hooks**, **scripts**, **VS Code tasks**, **guides** (CLAUDE.md / AGENT.md packs)
and **bundles** of these — and a **knowledge hub** for sharing write-ups. You can
install what others have published, and publish your own, so your team stops reinventing the same
prompts and configs on every project.

## Marketplace — skills & subagents

Open **Marketplace** from the app to browse, install and manage packages.

### Official packages

Packages published by 4PM carry an **Official** badge; use the **Official only** filter to see just
those.

### Install a package

- **Search** the catalog and **Install** a package into a project or your org. Installed packages
  are listed under **Installed packages** with their version.
- **Claude and/or Codex:** for skills, subagents and hooks, choose which AI to install for. You're warned
  when the project's worker has no profile for that AI.
- **Dependencies:** installing a package also installs what it requires; removing one that others still
  need asks first.
- **Hooks are reviewed:** every hook command is shown and must be confirmed before install. Hooks from
  other organizations stay off unless an ADMIN allows them in Settings.
- **Guide packages:** **Adapt with AI** rewrites your CLAUDE.md or AGENT.md to fit your project and shows
  the changes for you to edit and accept.
- **Auto-update** — turn on "Auto-update packages to the latest approved version" to keep installs
  current, or update each one manually when an **Update to v{version}** badge appears.
- **Locally edited** ("drift") — if a package was changed on the worker after install, it's flagged
  so you know it differs from the published version.
- **Remove** an install at any time; existing project files stay unless you remove them.

### Publish a package

You can publish two ways:

- **Upload a zip** — Marketplace › **Publish a package**. Works for every kind.
- **Publish a bundle from a project** — Content › AI content › **Packages** › **Publish bundle**: pick several of the
  project's subagents, skills and Claude commands (names in `.claude/commands`) and publish them as one
  package with one version. Scripts, VS Code tasks and hooks still go through a zip.

Publishing needs the **Pro** plan or higher.

#### The package zip

At the root of the zip put a manifest named **`4pm-package.json`**, plus the payload files:

```json
{
  "schema": 1,
  "kind": "skill",
  "slug": "secret-scan",
  "name": "Secret scan",
  "version": "1.0.0",
  "description": "Scans the repo for leaked secrets",
  "author": "Your team",
  "changelog": "First release",
  "providers": ["claude", "codex"],
  "requires": ["script:git-prune-merged"]
}
```

- **kind**: `skill` · `subagent` · `command` · `hook` · `script` · `vscode-task` · `guide` · `bundle`.
- **slug**: the install name — letters, digits, `_`, `.`, `-` only. **version**: plain `MAJOR.MINOR.PATCH`.
- **providers** (skills, subagents, hooks): which AIs it works with — default Claude only.
- **requires**: other packages (`<kind>:<slug>`) installed together with it.

What the payload must contain, per kind:

| Kind | Payload | Installed to |
| --- | --- | --- |
| **Skill** | `SKILL.md` (frontmatter `name` = slug) + helper files; refer to them relative to the skill folder | `.claude/skills/<slug>/` (Codex: `.agents/skills/<slug>/`) |
| **Subagent** | `agent.md` (frontmatter `name` = slug), optional `short-memory.md` / `long-memory.md`; for Codex also `agent.codex.toml` | `.claude/agents/<slug>.md` (Codex: `.codex/agents/<slug>.toml`) |
| **Command** | exactly one `command.md` (Claude only) | `.claude/commands/<slug>.md` |
| **Hook** | `hook.json` (`{"hooks": {"<Event>": [{"matcher", "hooks": [{"type": "command", "command"}]}]}}`) + its scripts; write `{{hookDir}}` for the installed script folder | `.claude/hooks/<slug>/` + the project's hook settings |
| **Script** | any files, with a `README.md` | `.4pm/scripts/<slug>/` |
| **VS Code task** | exactly one `tasks.json` with only `{ "tasks": [...] }` (no tasks that run on folder open) | merged into `.vscode/tasks.json` |
| **Guide** | exactly one `GUIDE.md`, written generically | applied to CLAUDE.md / AGENT.md with **Adapt with AI** |
| **Bundle** | members listed as `<kind>:<slug>` (2 or more; no guides or bundles) | each member to its own place |

The [official packages repo](https://github.com/4azuo/4pm-public) has a working example of every kind.

#### Publish form

1. Choose the zip, a **scope** and optionally a **category**, **tags** and a **price** (USD, 0 = free).
2. Add a **thumbnail** and up to 10 **gallery** images (PNG, JPEG, WebP or GIF, 5 MB each) — now or later from
   the detail page.
3. **Publish.** Each publish of the same slug with a higher version adds a **version**. **Yank** a bad version
   (existing installs keep working) or **Unpublish** the package (installed copies stay on workers).

Scopes:

- **Personal** — only you. Live at once.
- **Organization** — everyone in your org. Live at once.
- **Global (public)** — every organization and the public store, after the approvals below.

Packages, images and Knowledge text count toward your organization's **hosted storage**; the per-file upload
limit follows your plan.

### Selling a package

Set a **price** above 0. Buyers pay **by card** (even without a 4PM account, on the public store) or **with
their credit balance** in the app; until then the content is locked ("Purchase to download"). Your own
organization never pays for its own package. Per sale **4PM keeps 10 %** and the seller's organization gets
**90 %** in its **credit balance** (Billing › Credit history), usable for plans, add-ons and rentals.

### Approval of global items

A global package version (or a global Knowledge post) goes through up to three steps:

1. **Your organization approves it.** It's **Pending review** until an ADMIN / PM of the publishing org opens
   **Moderation — pending global versions** in the Marketplace (Knowledge: **Pending review**) and
   **Approves** it or **Rejects** it with an optional reason. **Each new version** of a global package needs
   this approval again. Personal and organization scope skip this step.
2. **It becomes public** — visible to every org and on the public store.
3. **4PM reviews it.** An AI review and then a 4PM admin check public items. Until 4PM has allowed it,
   others see a caution. If the AI flags it, the owner (author and the org's ADMIN / PM) sees the reasons to
   fix; after an edit it shows *edited — waiting for re-review*. 4PM can **block** an item that breaks the
   platform rules: it disappears from every browse, download and install, and the owner is notified with the
   reason. Official 4PM packages skip this review.

Editing the public content (a new approved version, the name, description or tags) sends it back to 4PM's
review.

### Ratings & downloads

Packages show a **download count** and **reviews/ratings** (one per user, from people who downloaded it), so
you can judge quality before installing.

## Public storefront

There's also a **public marketplace** (no login required) where anyone can browse global-approved
packages, read reviews, download free packages, and buy paid ones by card. The signed-in
Marketplace inside the app is the same catalog with your installs and publishing tools added.

## Knowledge hub

The **Knowledge** area is a lightweight place to share distilled know-how as **Markdown posts**:

- Write a post with a **title**, optional **summary**, **category** and **tags**.
- Choose a **scope** (Personal / Organization / Global public), and add a cover image and a gallery if you
  like. Global posts follow the same [approval steps](#approval-of-global-items) as packages: your org's
  admins approve them under **Pending review**, then 4PM reviews them once public.
- **Share as knowledge** from a project (its action bar / Market tab): the AI distils the project's
  know-how into a draft post, which opens in the Knowledge editor for you to review and publish.
- Browse and **search** posts, sort by **newest / most viewed / top rated**, and leave
  **reviews/ratings**.

## Tips

- Publish stable, reusable prompts as **Skills** and specialized agent configs as **Subagents** so
  new projects start from a known-good baseline.
- Use **Organization** scope for internal building blocks and **Global** only for things you want
  to share publicly (and are happy to have moderated).
- Keep versions small and yank rather than delete when something's wrong — installs keep working.

See also: [Marketplace & knowledge FAQ](../faq/marketplace.md).
