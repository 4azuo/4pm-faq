# Marketplace & knowledge hub

4PM has a built-in **marketplace** for reusable agent building blocks — **skills** and
**subagents** (and `CLAUDE.md` packs) — and a **knowledge hub** for sharing write-ups. You can
install what others have published, and publish your own, so your team stops reinventing the same
prompts and configs on every project.

## Marketplace — skills & subagents

Open **Marketplace** from the app to browse, install and manage packages.

### Install a package

- **Search** the catalog and **Install** a package into a project or your org. Installed packages
  are listed under **Installed packages** with their version.
- **Auto-update** — turn on "Auto-update packages to the latest approved version" to keep installs
  current, or update each one manually when an **Update to v{version}** badge appears.
- **Locally edited** ("drift") — if a package was changed on the worker after install, it's flagged
  so you know it differs from the published version.
- **Remove** an install at any time; existing project files stay unless you remove them.

### Publish a package

1. Prepare your package as a **zip** and click **Publish a package**.
2. Choose a **kind** (Skill or Subagent) and a **scope**:
   - **Personal** — only you.
   - **Organization** — everyone in your org.
   - **Global (public)** — visible across all orgs **after** your org's ADMIN/PM approve the
     version (see moderation below).
3. Publish. Each publish creates a **version**; you can **Yank** a bad version (existing installs
   keep working) or **Unpublish** the package (installed copies stay on workers).

### Moderation (going public)

Global packages don't go public instantly. An **ADMIN/PM** in your org reviews pending global
versions in the **Moderation** queue and **Approves** or **Rejects** them. Only approved versions
become public across orgs.

### Ratings & downloads

Packages show a **download count** and **reviews/ratings** from users, so you can judge quality
before installing.

## Public storefront

There's also a **public marketplace** (no login required) where anyone can browse global-approved
packages, read reviews, download free packages, and buy paid ones by card. The signed-in
Marketplace inside the app is the same catalog with your installs and publishing tools added.

## Knowledge hub

The **Knowledge** area is a lightweight place to share distilled know-how as **Markdown posts**:

- Write a post with a **title**, optional **summary**, **category** and **tags**.
- Choose a **scope** (Personal / Organization / Global public). Global posts are **reviewed by your
  org's admins** before they go public.
- Browse and **search** posts, sort by **newest / most viewed / top rated**, and leave
  **reviews/ratings**.

## Tips

- Publish stable, reusable prompts as **Skills** and specialized agent configs as **Subagents** so
  new projects start from a known-good baseline.
- Use **Organization** scope for internal building blocks and **Global** only for things you want
  to share publicly (and are happy to have moderated).
- Keep versions small and yank rather than delete when something's wrong — installs keep working.

See also: [Marketplace & knowledge FAQ](../faq/marketplace.md).
