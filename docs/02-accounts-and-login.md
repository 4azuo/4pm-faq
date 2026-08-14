# Accounts, organizations & login

Everything in 4PM lives under an **organization**. Registering creates both your org and its
first user; other people join as users inside that org.

## Register

Registration creates a new **organization** plus its first **root** user (an ADMIN).

1. Go to the register page and enter a **username**, **email**, **password**, optionally a
   **phone**, and an optional **IP allowlist** (leave it empty to allow any IP).
   - Username and email must be unique.
2. Optionally **pick a plan and payment method**. Choosing a paid plan (e.g. **Pro**) shows a
   provider picker (Stripe / PayPal). Your org is always created on the **Free** plan first; the
   paid plan is remembered and checkout opens automatically after you verify and log in.
3. Submit. 4PM sends a **verification email** with a link.
4. **Open the link to verify your email.** You cannot log in until your email is verified.

For anti-abuse reasons, registration and password-reset always return the same neutral response
regardless of whether the address exists.

## Log in

There are **two login modes**:

- **Root user** — leave the *Organization Identifier* field **empty**. Root login requires MFA.
- **Organization user (non-root)** — enter your org's **Organization Identifier** (a UUID your
  admin gives you) along with your username/email and password.

Steps:

1. Enter username/email + password (and the Organization Identifier if you're an org user).
2. The server checks account lockout, your password, that your email is verified, and your IP
   allowlist.
3. **Root ⇒ MFA is mandatory.** You receive a **6-digit one-time code** by email (valid ~5
   minutes, limited attempts). Enter it to finish logging in. Non-root users are logged in
   directly.

There is no "remember password" option. Sessions refresh automatically; once the refresh window
expires (7 days by default) you'll need to log in again.

## Multi-factor authentication (MFA)

- **Root** users always go through the email OTP step at login.
- The code is single-use and expires quickly. If you mistype it too many times, request login
  again.

## Sign in with Google or GitHub (SSO)

Instead of a password you can use **single sign-on**:

- **Sign in with Google** or **Sign in with GitHub** from the login page — the provider verifies
  your identity and you're logged straight in, no password step.
- **Register from a provider:** the register form can **start from** Google or GitHub. The provider
  verifies your email, then you complete the register step to create your org — because the email is
  already provider-verified, there's no separate verification email to open.
- An SSO account created this way has **no password**; sign back in with the same provider (you can
  add a password later from account settings if you want one).

> **SAML** (per-organization enterprise IdP) is planned but **not enabled yet** — today SSO is
> Google and GitHub.

## Roles & permissions

Access is controlled by **roles** granted to each user, for example:

- **ADMIN** — full control of the org (billing, users, projects, settings).
- **PM (Project Manager)** / **TL (Team Lead)** — manage projects and teams they're scoped to.
- **SA/SE, QA, BA** — contributor roles with read and task-specific permissions.
- **MACHINE** — the role a paired worker CLI runs as, scoped to its project.

If an action is blocked, you're likely missing the required permission for it — ask an ADMIN or
PM in your org to grant it.

## Organizations & users

- An **ADMIN** invites/creates users, assigns roles, and manages teams and projects.
- Users only see the projects and machines they're a member of or scoped to.
- Platform-level administration (across all orgs) is a separate surface operated by the 4PM
  platform team — not something org users access.

## Common issues

- **"Can't log in right after registering"** — verify your email first via the link.
- **"Invalid credentials with a valid password"** — check you're using the right login mode
  (empty Organization Identifier for root; correct UUID for org users).
- **"Account locked"** — too many failed attempts; wait and try again, or ask an ADMIN.

See also: [Password & account recovery FAQ](../faq/account-and-login.md).
