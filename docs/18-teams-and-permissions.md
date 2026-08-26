# Teams, members & permissions

Organize people into **teams**, control what they can do with **permissions**, and bring new
people in with **invitations**.

## Teams

A **team** groups human users and the projects they work on. On a team's page you can:

- See the team **info** and activity stats.
- Manage **members** — attach or detach users (a confirmation dialog shows what a user is attached
  to before you detach them). Machine users and ADMINs aren't team members.
- Manage the team's **projects** — attach or detach.
- Set a **Team Lead (TL)** — one lead per team; the lead gets a badge.
- Edit team **settings** (name, team-level IP allowlist) and, in the danger zone, **delete** the
  team (you type the team's id to confirm).
- Upload a team **avatar**.

Non-managers see the team's Info only; the Settings and Permission tabs are for managers (and the
lead can edit team settings).

## Permissions

Access is controlled by **permissions** granted to a **subject** — a user, a team, or a project.
On the Permissions screen you:

1. Pick the subject (user / team / project).
2. For each permission, set **allow**, **deny**, or **inherit**.

- Resolution order is **project → team → user** — a more specific grant wins.
- **ADMIN** can set grants for users, teams and projects; **PM** can set them for projects only;
  other roles view the catalog read-only.
- There's a searchable **matrix** view and a **JSON** view for bulk edits.
- The **root** user isn't listed — it's fully privileged and can't be edited.

If an action is blocked for you, you're likely missing a permission — ask an ADMIN or PM to grant
it. The permission matrix is also embedded in each user/team/project page.

## Invitations — joining an org

An ADMIN invites people by email. As an invitee:

1. Open the **invite link** in the email.
2. You'll see the organization, your email and the roles you'll get.
3. Set a **username** and **password** — your account is created (email already verified) and you
   go straight into the app.

If the link is broken or expired, you'll see an invalid-link message; ask your ADMIN to re-send.

See also: [Accounts & login](./02-accounts-and-login.md) ·
[Teams & permissions FAQ](../faq/teams-and-permissions.md).
