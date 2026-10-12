# Accounts & login

**How do I sign up?**
Register with a username, email and password. This creates your **organization** and its first
**root** user, and sends a verification email. Details:
[docs/02](../docs/02-accounts-and-login.md).

**Can I sign in with Google or GitHub?**
Yes. Use **Sign in with Google** or **Sign in with GitHub** on the login page — the provider
verifies you and logs you in without a password. You can also **start registration** from a
provider (it verifies your email, so no verification mail is needed). SSO accounts have no
password; sign back in with the same provider. **SAML** (enterprise IdP) is planned but not
enabled yet. See [docs/02](../docs/02-accounts-and-login.md#sign-in-with-google-or-github-sso).

**Why can't I log in right after registering?**
You must **verify your email** first via the link 4PM sends (email/password sign-up only). Login
isn't possible before verification.

**I have the right password but login fails — why?**
Check your **login mode**. Leave the *Organization Identifier* empty to log in as the **root**
user; enter your org's **Organization Identifier** (its UUID or its login alias) to log in as an org
user. Using the wrong mode returns an invalid-credentials error.

**What's the "Organization Identifier"?**
The value that identifies your organization at login — either the org's UUID or its short
**login alias** (an ADMIN sets the alias in the Organization tab). Org (non-root) users need it; an
ADMIN can provide it. Root users leave it empty.

**Why am I asked for a code or a passkey at login?**
That's **two-factor authentication (2FA)**. You're asked for it when you've set up a factor (an
authenticator app or a passkey), when your organization requires 2FA, and always for the **root**
user (root can also get a one-time code by email as a backup). See
[docs/02](../docs/02-accounts-and-login.md#two-factor-authentication-2fa).

**I'm asked to set up two-factor authentication before I can log in.**
Your ADMIN requires 2FA (for ADMINs or for everyone). Scan the QR code with an authenticator app, or
register a passkey — finishing the setup logs you in. Save the **recovery codes** you're shown.

**I lost my phone / authenticator.**
Log in with one of your **recovery codes** (each works once). If you have none left, ask an
**ADMIN** to reset your 2FA; you'll set it up again at your next login.

**My account is locked.**
After 5 wrong passwords from the same network, sign-in from that network is locked for 15 minutes
(longer if it repeats). Wait and retry, or try from your usual network, or ask an ADMIN.

**How do I reset my password?**
Click **Forgot password** on the login page and enter your Organization Identifier (empty for root),
your username and your email or phone. 4PM emails a reset link valid for **15 minutes**. For
security, the response is the same whether or not the account exists. Accounts without an email ask
their **ADMIN** to set a new password.

**I'm told my password has expired.**
Your organization has a password expiry. Set a new password (different from the old one) on the
screen shown at sign-in; you get reminders during the last 7 days.

**What are the password rules?**
12–128 characters of any kind — a passphrase works well. Passwords found in known data breaches are
refused.

**How long do sessions last?**
Sessions refresh automatically; by default the refresh window is 7 days, after which you log in
again. There is no "remember password" option.

**Why is an action blocked for me?**
You're probably missing the **permission** for it. Roles (ADMIN, PM, TL, etc.) grant permissions —
ask an ADMIN or PM to grant what you need. See [docs/02](../docs/02-accounts-and-login.md#roles--permissions).
