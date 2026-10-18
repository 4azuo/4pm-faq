# Marketplace & knowledge hub — FAQ

**What's in the marketplace?**
Reusable **skills**, **subagents**, **Claude commands**, **hooks**, **scripts**, **VS Code tasks**,
**guides** (CLAUDE.md / AGENT.md) and **bundles**, including **Official** 4PM packages, plus a
**knowledge hub** of shared Markdown write-ups. See
[Marketplace & knowledge hub](../docs/13-marketplace.md).

**How do I install a package?**
Open **Marketplace**, search, and click **Install**. Installed packages appear under **Installed
packages**; turn on **Auto-update** to track the latest approved version.

**Can I install a package for Codex instead of Claude?**
Yes — for skills, subagents and hooks, choose Claude and/or Codex when installing. You're warned if the
project's worker has no profile for that AI.

**Why must I confirm each hook command?**
Hooks run commands on the worker, so every hook command is shown for review before install. Hooks from
other organizations stay off unless an ADMIN allows them in Settings.

**What does "Adapt with AI" do on a guide package?**
The AI rewrites your project's CLAUDE.md or AGENT.md to fit the project and shows the changes for you
to edit and accept.

**How do I publish my own?**
Marketplace › **Publish a package**: choose a zip, a **scope** (Personal / Organization / Global public),
optionally a category, tags, a price and images, then **Publish** (Pro plan or higher). To publish several
of a project's subagents, skills and commands together, use Content › AI content › **Packages** ›
**Publish bundle**. See [docs/13](../docs/13-marketplace.md#publish-a-package).

**What goes in the zip?**
A **`4pm-package.json`** manifest at the root (`schema: 1`, `kind`, `slug`, `name`, `version` as
`MAJOR.MINOR.PATCH`, and optionally `description`, `author`, `changelog`, `providers`, `requires`) plus the
payload: `SKILL.md` for a skill, `agent.md` for a subagent, `command.md`, `hook.json` + scripts, `tasks.json`,
`GUIDE.md`… The table per kind is in [docs/13](../docs/13-marketplace.md#the-package-zip); the official
packages repo has an example of each.

**My upload is refused ("missing 4pm-package.json", "bad slug", "bad version").**
The manifest must sit at the zip root (not inside a folder), be valid JSON, use a slug of letters, digits,
`_ . -` only, and a plain three-part version (no `-beta`). A new release needs a **higher** version.

**How do I release a new version?**
Publish a zip with the same slug and a higher version. Installs with **Auto-update** pick up the newest
approved version; others see an **Update to v…** badge.

**What does "Global (public)" mean, and who approves it?**
The package becomes visible to every organization and on the public store, in steps:
1. **Your org approves** — it's *Pending review* until an ADMIN / PM approves it in Marketplace ›
   **Moderation — pending global versions** (or rejects it with a reason). Every new version needs this.
2. It goes **public**.
3. **4PM reviews** it (AI review, then a 4PM admin). Others see a caution until 4PM has allowed it; 4PM can
   **block** it if it breaks the platform rules (you're notified with the reason).
Personal and organization packages are live at once, without approvals.

**My package was rejected / blocked — what now?**
*Rejected* (by your org): read the reason, fix it and publish a new version. *Blocked* (by 4PM): it's hidden
from every browse, download and install; fix what the notice says, then contact support to have it
reviewed again.

**Can I sell a package?**
Yes — set a **price** (USD, 0 = free) when publishing. Buyers pay by card (even without an account, on the
public store) or with their credit balance. 4PM keeps **10 %**; **90 %** goes to your organization's
**credit balance** (Billing › Credit history), usable for plans, add-ons and rentals. There's no bank payout.

**Do I have to buy my own organization's paid package?**
No — your own organization always has access.

**Can I take a package back?**
**Yank** a bad version (existing installs keep working) or **Unpublish** the package (copies
already on workers stay). 

**What's "Locally edited" / drift?**
The installed files were changed on the worker after install, so they differ from the published
version. Update to re-sync, or keep your local edits.

**Is there a public store without an account?**
Yes — the public marketplace lets anyone browse global packages, read reviews, download free ones
and buy paid ones by card. Signing in adds your installs and publishing tools.

**What's the knowledge hub?**
A place to publish **Markdown posts** (title, summary, category, tags, cover and gallery images) at
Personal / Org / Global scope, with search, sorting and star ratings.

**How do I publish a Knowledge post?**
Knowledge › **New post**: write it in Markdown in the dialog, pick a category, tags and scope, add images,
then **Publish**. Or, from a project, **Share as knowledge**: the AI distils the project's know-how into a
draft that opens in the editor for you to review and publish.

**Who approves a global Knowledge post?**
The same steps as packages: your org's admins approve it under **Pending review** (or reject it with a
reason), then it's public and 4PM reviews it.

**How do I find packages that work with my AI?**
The Marketplace is a store: a featured shelf, a filter sidebar (which AI a package works with — Claude,
Codex or any — and free / paid) and cards with rating and price.

**How do I add a thumbnail or screenshots?**
Upload a thumbnail and gallery images when you publish a package or Knowledge post, or later from its
detail page. They count toward your organization's hosted storage.

**My package / post shows a 4PM AI review warning.**
Public packages, Knowledge articles and 4rum posts are checked by 4PM's AI review. As the owner you see why
it was flagged so you can fix it; others see a caution until 4PM has checked it. After you edit, it shows
"edited — waiting for re-review".

**Does Marketplace content use our storage?**
Yes — packages, images and Knowledge post text count toward your organization's hosted storage
(Settings › Storage lists them separately), and the per-file upload limit follows your plan.

See also: [Marketplace & knowledge hub](../docs/13-marketplace.md).
