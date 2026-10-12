# Your account & settings

Open your own profile from the user menu to reach the **Settings** tab, where you manage your
display name, avatar, password, contact details and linked sign-in accounts. You always see the
Settings tab on **your own** profile; an **ADMIN** sees it on other users too (to manage them).

## Display name & avatar

- Your **username** is fixed, but you can set a friendly **display (alias) name** that's shown in
  its place across the app.
- Upload or remove your **avatar** (only on your own profile).

## Change your password

In the **Security** section, change your password by entering your **current** password and a new
one. For safety this **sends a confirmation email** — the change takes effect once you confirm via
the link, not immediately.

> An **ADMIN** can also reset another user's password directly (that logs the user out of their
> sessions). You can't reset your own or the root user's password this way — use the Security
> section above.

## Change your email or phone

You change contact details through a **verified** flow, **one field at a time**:

- **Change email** — 4PM sends a **one-time code to your phone**; enter it to confirm.
- **Change phone** — 4PM sends a **link to your email**; open it to confirm.

While a change is pending you'll see the pending request and a **Cancel** button.

## Linked sign-in accounts (Google / GitHub)

- **Connect** Google or GitHub so you can sign in with that provider.
- **Disconnect** one you no longer use — but you can't remove your **last** remaining sign-in
  method (that would lock you out).

If you registered via SSO and have no password, you can add one here so you also have a
password login.

## Two-factor authentication & passkeys

In the **Security** panel you can set up an **authenticator app**, register **passkeys**, and view or
regenerate your **recovery codes** (regenerating or removing a factor asks for your password). You can't
remove your last factor while your organization requires 2FA. See
[Accounts & login](./02-accounts-and-login.md#two-factor-authentication-2fa).

## Idle screen lock & unlock PIN

After a period of inactivity set by your ADMIN for the whole organization, the app **locks**: your work
is hidden behind a lock screen and the session can't be used until you unlock it with your **password**
or an optional **PIN** (4–12 digits). Set or remove the PIN in the **Security** panel.

## Display preferences

From the settings menu you can choose the **language** (English, Tiếng Việt, 日本語, 中文), the
**appearance** (light / dark / system) and the **theme** (Default, Flat, 8-bit). Every table also has a
settings gear to remember its rows per page, sort and filters.

## Finding things quickly

- **Global search** (header): projects, teams, people, issues, tasks, milestones, docs, Messenger
  channels, chats and 4rum posts in one box.
- **Pin** projects and teams to keep them at the top of your Overview; recently opened projects are listed
  too.
- **What's new** (footer) lists the latest changes and what's coming soon.

## API clients

In **Settings › API clients** you create clients that let your own scripts and tools use 4PM through the
public API. A client acts as you, limited to the scopes you choose, and can never approve anything — see
[Public API & API clients](./32-public-api.md).

## IP allowlist

Your account can be restricted to certain IPs. Only an **ADMIN** (or a manager of your account)
can edit an allowlist; a regular user can't change their own. An allowlist must stay within your
organization's (and any team/project) allowlist. If you're blocked by IP, ask an ADMIN.

See also: [Accounts & login](./02-accounts-and-login.md) ·
[Account settings FAQ](../faq/account-settings.md).
