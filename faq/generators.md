# Generators & doc types

**How do I generate a document (report, estimate, proposal…)?**
Project › **Generators** › **Generate**: pick a doc type, fill in its parameters, choose a template and
generate. The document is saved even if you leave the page. See
[docs/30](../docs/30-generators-and-doc-types.md).

**I don't see a doc type / the Generators tab.**
You can only see the doc types you're allowed to **run** or **view**. Ask an ADMIN/PM to add you to its
run access, or to attach and enable the type in the project.

**Can I create my own kind of document?**
Yes — create a **doc type** (instructions, parameters, templates) in Home › Docs templates › Doc types,
or a project-only one in the project's Generators › Doc types. Built-in types (Report, Estimation, WBS,
Proposal, Feasibility) can be **forked** and edited.

**How do I share a generated document with my customer?**
Add the customer to the doc type's **view access** in the project. They then see its documents
read-only.

**Does generating use my AI quota?**
Yes — it's an AI run on the project's workers, using a run slot and quota.

## Doc templates for the docs round

**What are "Doc templates"?**
The templates the autonomous **docs round** follows when it writes a request's docs (ADRs, API specs, screen
specs… — the doc types your spec declares). Each one has a **template file** (one text file — md / txt / html,
up to 64 KB), **instructions** for the AI, and whether its files are **numbered** (`0001-slug.md`) or named by
slug. Find them in Project › Content › AI content › **Doc templates**.

**How are they different from Generator doc types?**
Same library, different **usage**: a *generator* doc type makes a report on demand in Generators; a *spec* doc
type steers the docs round. Generators › Doc types lists only generator types; AI content › Doc templates lists
only spec types.

**Where do organization-wide templates live?**
Home › **Docs templates** › Doc types (filter by usage). A project attaches them, forks them or adds its own —
at most **one enabled** template per doc type.

**Where does the AI read them from?**
Saving, enabling or disabling a template commits it to the repo under `.4pm/doc-templates/<type>/`
(`meta.json`, `instructions.md`, the template file), so every worker uses the same version. Disabling removes
the folder. A new doc type key you type in the editor is added to the spec's doc types for you.

**Do new numbered docs clash between requests?**
No — numbers are reserved per request, so two open requests never write the same `0042-…` file.

