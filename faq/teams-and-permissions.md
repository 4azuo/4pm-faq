# Teams, members & permissions

**What's a team?**
A group of human users and the projects they work on. On a team's page you manage members,
projects, the settings, and one **Team Lead (TL)**. See [docs/18](../docs/18-teams-and-permissions.md).

**How do I add or remove team members?**
From the team's **Members** — attach or detach users (a confirmation shows what they're attached to
before you detach). Machine users and ADMINs aren't team members.

**How do permissions work?**
Permissions are granted to a **subject** (user, team or project) as **allow / deny / inherit**.
Resolution is **project → team → user** (more specific wins). See
[docs/18](../docs/18-teams-and-permissions.md#permissions).

**Who can set permissions?**
**ADMIN** can set grants for users, teams and projects; **PM** for projects only; other roles view
the catalog read-only. The **root** user isn't editable and isn't listed.

**Why is an action blocked for me?**
You're probably missing a permission for it — ask an ADMIN or PM to grant it. The permission matrix
is also embedded in each user/team/project page.

**How do I join an organization I was invited to?**
Open the **invite link** in your email, review the org/email/roles, then set a **username** and
**password** — your account is created (email already verified) and you go straight in. A broken or
expired link shows an invalid-link message; ask your ADMIN to re-send. See
[docs/18](../docs/18-teams-and-permissions.md#invitations--joining-an-org).

See also: [Teams, members & permissions](../docs/18-teams-and-permissions.md) ·
[Accounts & login](../docs/02-accounts-and-login.md).
