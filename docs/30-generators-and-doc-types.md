# Generators, doc types & templates

**Generators** produce project documents with AI — reports, estimates, WBS, proposals, feasibility
studies, or any kind of document your organization defines. Each kind is a **doc type**; doc types can
follow **template files**.

## Doc types

A doc type says what to generate:

- a **key** and **name**;
- **instructions** for the AI;
- **parameters** the person generating it is asked for;
- the **template files** it may follow, and a default one;
- default **run access** (who may generate it) and **view access** (who may read its documents).

**Built-in types:** Report, Estimation, WBS, Proposal, Feasibility. They can't be edited, but you can
**Fork** one to make your own version.

**Org doc types** live in Home › **Docs templates** › **Doc types** (ADMIN). **Template files** sit next to
them (Home › Docs templates › **Template files**) — versioned files with a description; re-uploading a
file with the same name keeps the older versions. Template files count toward your hosted storage.
Members who can't edit template files can submit a **change request** (see
[Checklists › Change requests](./26-checklists.md#change-requests)).

## In a project (Generators tab)

The **Generators** tab has three sub-tabs:

- **Generate** — pick one of the doc types you may run, fill in its parameters, choose a template, and
  generate. The run streams live (with your queue position if run slots are busy) and the document is
  **saved even if you leave the page**. Generated documents are listed below, filtered to the ones you
  may view.
- **Doc types** — attach built-in or org types, create project-only types, fork, turn each on or off,
  and set **who may generate** and **who may view** (by role or by member) and the default template.
  **Preview prompt** shows what the AI will receive.
- **Template files** — attach org template files, upload the project's own, or fork an org file, and
  choose which files the generators may use.

Changing doc types and templates needs the project's docs-manage permission (ADMIN/PM by default,
grantable to a member). Generating needs only to be in the type's **run access**. An empty view access
means every project member can read the documents. **Customers** can be given view access only — that's
how you share proposals or estimates with them.

## How generation runs

Generation runs on the project's workers as a **read-only** AI run: it uses a run slot and your quota,
reads the spec and the template, and saves the result as a project document pinned to the doc type and
template versions used.

## Generating from a rule

An [automation rule](./27-automation-rules.md) can generate a document when something happens — for
example a weekly report on a schedule.

See also: [Create & manage projects](./05-projects.md) · [Generators FAQ](../faq/generators.md).
