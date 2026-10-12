# Accounts, organizations & login

Everything in 4PM lives under an **organization**. Registering creates both your org and its
first user; other people join as users inside that org.

## Register

Registration creates a new **organization** plus its first **root** user (an ADMIN).

1. Go to the register page and enter a **username**, **email**, **password**, optionally a
   **phone**, and an optional **IP allowlist** (leave it empty to allow any IP).
   - Username and email must be unique.
   - The password needs **12–128 characters** of any kind (a passphrase works well). Passwords found
     in known data breaches are refused.
2. Optionally **pick a plan and payment method**. Choosing a paid plan (e.g. **Pro**) shows a
   provider picker (Stripe / PayPal). Your org is always created on the **Free** plan first; the
   paid plan is remembered and checkout opens automatically after you verify and log in.
3. Submit. 4PM sends a **verification email** with a link.
4. **Open the link to verify your email.** You cannot log in until your email is verified.

For anti-abuse reasons, registration and password-reset always return the same neutral response
regardless of whether the address exists.

## Log in

There are **two login modes**:

- **Root user** — leave the *Organization Identifier* field **empty**.
- **Organization user (non-root)** — enter your org's **Organization Identifier** — the org's UUID
  **or** its short **login alias** (an ADMIN sets the alias in the Organization tab) — along with
  your username/email and password.

Steps:

1. Enter username/email + password (and the Organization Identifier if you're an org user).
2. The server checks your password, account lockout, that your email is verified, and your IP
   allowlist.
3. If you have a **second factor**, or your organization requires one, you're asked for it (see
   below). Otherwise you're logged in.
4. If your organization has a **password expiry** and your password has expired, you're asked to set a
   new one (it must differ from the old one) before you get in.

There is no "remember password" option. Sessions refresh automatically; once the refresh window
expires (7 days by default) you'll need to log in again.

## Two-factor authentication (2FA)

You can protect your sign-in with a second factor, managed from the **Security** panel of your
profile:

- **Authenticator app** (TOTP — Google Authenticator, 1Password, Authy…): a 6-digit code that changes
  every 30 seconds.
- **Passkey** — your device's fingerprint/face/PIN or a security key. You can register several.
- **Recovery codes** — 10 one-time codes issued when you set up your first factor. Keep them somewhere
  safe; each works once. You can regenerate them (needs your password).

How it applies:

- Once you set up a factor, you're **always** asked for it at login (password or Google/GitHub).
- An ADMIN can **require** 2FA in **Organization Settings › Security**: for **ADMINs only** (the
  default), for **everyone**, or off. If it's required and you have no factor yet, you set one up at
  your next sign-in — finishing the setup logs you in.
- The **root** user always needs a second factor. Root can also receive a **one-time code by email**
  as a backup.
- Worker (machine) accounts are exempt.
- **Lost your device?** Use a recovery code. If you have none left, ask an **ADMIN** to reset your
  2FA — you're signed out and notified, then you set it up again at the next login.

## Forgot your password

On the login page choose **Forgot password**:

1. Enter your **Organization Identifier** (empty for root), your **username**, and your **email or
   phone**.
2. If the account exists and has a verified email, 4PM emails a **reset link** (valid **15
   minutes**).
3. Open the link and set the new password.

Accounts without an email (some internal sub-accounts) can't self-reset — ask your **ADMIN**, who can
set a new password for you.

## Password expiry

An ADMIN can set a **password expiry** (in days) in **Organization Settings › Security**. You get a
reminder during the last 7 days, and once it expires you must set a new password at sign-in. It
doesn't apply to root, to SSO-only accounts or to worker accounts.

## Sign in with Google or GitHub (SSO)

Instead of a password you can use **single sign-on**:

- **Sign in with Google** or **Sign in with GitHub** from the login page — the provider verifies
  your identity and you're logged straight in (plus your second factor, if you have one).
- **Register from a provider:** the register form can **start from** Google or GitHub. The provider
  verifies your email, then you complete the register step to create your org — because the email is
  already provider-verified, there's no separate verification email to open.
- An SSO account created this way has **no password**; sign back in with the same provider (you can
  add a password later from account settings if you want one).
- Sign-in must **finish in the same browser** it was started in — opening the provider link in another
  browser fails on purpose (it blocks hijacked sign-ins).

> **SAML** (per-organization enterprise IdP) is planned but **not enabled yet** — today SSO is
> Google and GitHub.

## Roles & permissions

Access is controlled by **roles** granted to each user, for example:

- **ADMIN** — full control of the org (billing, users, projects, settings).
- **PM (Project Manager)** / **TL (Team Lead)** — manage projects and teams they're scoped to.
- **SA/SE, QA, BA** — contributor roles with read and task-specific permissions.
- **CLIENT (customer)** — an outside customer you invite to specific projects. Sees only those
  projects, mostly read-only, and can post requests and answer the AI's questions. See
  [Customer accounts](./29-customer-accounts.md).
- **MACHINE** — the role a paired worker CLI runs as, scoped to its project.

ADMIN, CLIENT and MACHINE are **exclusive** roles (a user with one of them has no other role). If an
action is blocked, you're likely missing the required permission for it — ask an ADMIN or PM in your
org to grant it. See [Teams, members & permissions](./18-teams-and-permissions.md).

## Organizations & users

- An **ADMIN** invites/creates users, assigns roles, and manages teams and projects.
- Users only see the projects and machines they're a member of or scoped to.
- Platform-level administration (across all orgs) is a separate surface operated by the 4PM
  platform team — not something org users access.

## Account protection

- **Lockout:** after 5 wrong passwords from the same network, sign-in from that network is locked for
  15 minutes (longer if it keeps happening). Wrong passwords tried from **another** network don't lock
  you out. A wrong password never reveals whether an account exists.
- **Idle screen lock:** after the idle time your ADMIN sets, the app locks until you enter your password
  or your unlock **PIN** (see [Your account & settings](./16-account-settings.md#idle-screen-lock--unlock-pin)).

## Common issues

- **"Can't log in right after registering"** — verify your email first via the link.
- **"Invalid credentials with a valid password"** — check you're using the right login mode
  (empty Organization Identifier for root; the org UUID or alias for org users).
- **"Account locked"** — too many failed attempts from your network; wait and try again, or ask an
  ADMIN.
- **"Asked to set up two-factor authentication"** — your org requires 2FA; set up an authenticator app
  or a passkey to continue.
- **"Lost my authenticator"** — use a recovery code, or ask an ADMIN to reset your 2FA.

See also: [Password & account recovery FAQ](../faq/account-and-login.md).
